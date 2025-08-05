# 🚀 Jenkins CI/CD Pipeline Project (GitHub + Docker)

Created By:Abhishek Mishra  
GitHub Repo: [jenkins-pipeline-demo](https://github.com/Abhi-mishra998/jenkins-pipeline-demo)



## 📌 Project Objective

Set up a **complete Jenkins CI/CD pipeline** that:
- Pulls code from a GitHub repo
- Builds a Docker image
- Simulates testing and deployment
- Uses a `Jenkinsfile` from source control (Pipeline as Code)

---

## 📁 Repository Structure

```
jenkins-pipeline-demo/
├── Dockerfile
├── app.js
├── package.json
└── Jenkinsfile ✅
```


## 🔁 Pipeline Workflow

The Jenkins pipeline includes the following stages:

| Stage    | Description                        |
|----------|------------------------------------|
| 🛠️ Build   | Builds Docker image from Dockerfile |
| 🧪 Test    | Simulates unit tests               |
| 🚀 Deploy  | Simulates application deployment   |



## 💥 Challenges Faced & Resolved

### 1. 🔐 GitHub Token Credential Issue
- Jenkins failed to fetch private repo due to missing token.
- Solution: Created a [GitHub Personal Access Token](https://github.com/settings/tokens), then:
  - Navigated to `http://localhost:8080/manage/credentials/store/system/`
  - Added new credentials with token
  - Selected that credential in the pipeline job

### 2. 🐳 Docker Permission Denied Error
- Error:
  ```
  ERROR: permission denied while trying to connect to the Docker daemon socket
  ```
- **Cause:** Jenkins user didn’t have Docker permissions
- **Solution:** Added Jenkins user to Docker group:
  ```bash
  sudo usermod -aG docker jenkins
  sudo systemctl restart docker
  ```

### 3. 🌐 **GitHub SCM Fetch Failure**
- Error:
  ```
  fatal: couldn't find remote ref refs/heads/master
  ```
- **Cause:** GitHub repo had only `main` branch
- **Solution:** Updated branch specifier in Jenkins config to `main`



## 📄 Jenkinsfile (Pipeline as Code)

```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-app"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the app...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "Tests passed!"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the app...'
                sh 'echo "App deployed successfully!"'
            }
        }
    }
}
```


## ✅ Final Pipeline Status

- Jenkins successfully pulled code from GitHub using SCM
- Docker image built without errors
- All stages (`Build`, `Test`, `Deploy`) completed
- ✅ Final result: `SUCCESS`**



## 🖥️ Console Output Snapshot

```text
Started by user Abhishek Mishra
...
[Pipeline] stage (Build)
+ docker build -t my-app .
...
[Pipeline] stage (Test)
+ echo "Tests passed!"
...
[Pipeline] stage (Deploy)
+ echo "App deployed successfully!"
Finished: SUCCESS
```
## 📌 Tools Used

| Tool        | Purpose                          |
|-------------|----------------------------------|
| Jenkins     | CI/CD Automation                 |
| Docker      | Containerization                 |
| GitHub      | Source Code Management           |
| Git         | Code Checkout via SCM Plugin     |
| Bash        | Fix permission and setup issues  |

## 📦 Result
🎉 You have a working Jenkins CI/CD pipeline that builds, tests, and deploys a Dockerized Node.js app — ready to be added to your resume and portfolio!
