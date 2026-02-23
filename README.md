# Module 8 - Build Automation & CI/CD with Jenkins

This repository contains a demo project created as part of my **DevOps studies** in the **TechWorld with Nana – DevOps Bootcamp**.

https://www.techworld-with-nana.com/devops-bootcamp

***Demo Project:*** Create a Jenkins Shared Library

***Technologies used:*** Jenkins, Groovy, Docker, Git, Java, Maven

***Project Description:*** 

Create a Jenkins Shared Library to extract common build logic:

- Create separate Git repository for Jenkins Shared Library project
- Create functions in the JSL to use in the Jenkins pipeline
- Integrate and use the JSL in Jenkins Pipeline (globally and for a specific project in Jenkinsfile)

---

### Create separate Git repository for Jenkins Shared Library project

Name: `jenkins-shared-library`

![](./images/jenkins-shared-library.png)

Repository URL: `https://github.com/explicit-logic/jenkins-shared-library`

### Make Shared Library available globally

- Navigate to `Manage Jenkins` -> System -> Global Trusted Pipeline Libraries

- Click `Add`

Name: `jenkins-shared-library`

Default version: `main`

Retrieval method: `Modern SCM`

Source Code Management: `Git`

Project Repository: `https://github.com/explicit-logic/jenkins-shared-library`

Credentials: `github`

Click **Save**.

### Integrate and use the JSL in Jenkins Pipeline (globally and for a specific project in Jenkinsfile)

1. Create a `Multibranch Pipeline` Jenkins Job

- From the dashboard, click **New Item**
- Name: `microservice-user-auth`
- Type: **Multibranch Pipeline**
- Click **OK**

2. Configure Branch Sources

Under **Branch Sources**, click **Add source** > **Git** and fill in:

| Field | Value |
|-------|-------|
| Project Repository | `https://github.com/explicit-logic/jenkins-module-8.3` |
| Credentials | `github` |

Click **Save**. Jenkins will automatically scan the repository and create jobs for branches that contain a `Jenkinsfile`.

3. Run the job

Click **Build with Parameters** and fill in:

| Parameter | Value |
|-----------|-------|
| `DOCKER_IMAGE` | `<docker_username>/app` |

