#!/user/bin/env groovy
@Library('jenkins-shared-library')

def gv

pipeline {
  agent any
  tools {
    maven 'maven-3.9'
  }
  parameters {
    string(name: 'DOCKER_REPO', defaultValue: 'explicitlogic/app')
  }
  stages {
    stage("init") {
      steps {
        dir('app') {
          script {
            gv = load "script.groovy"
          }
        }
      }
    }

    stage("test") {
      when {
        expression {
          BRANCH_NAME == "main"
        }
      }
      steps {
        dir('app') {
          script {
            gv.testApp()
          }
        }
      }
    }

    stage("build jar") {
      steps {
        dir('app') {
          script {
            buildJar()
          }
        }
      }
    }

    stage("build image") {
      steps {
        dir('app') {
          script {
            buildImage(params.DOCKER_REPO, env.BRANCH_NAME)
          }
        }
      }
    }

    stage("deploy") {
      steps {
        dir('app') {
          script {
            gv.deployApp()
          }
        }
      }
    }
  }
} 
