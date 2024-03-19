# CI/CD Pipeline for Pet Clinic Application 🚀

## Introduction
This project aims to set up a CI/CD pipeline for the Pet Clinic application using Jenkins. The objective is to automate the build, test, and deployment processes, ensuring efficient software delivery and continuous integration and delivery.

## Step-by-Step Guide
### Note: Ensure JDK, Maven, Docker, and Jenkins are installed on your system.

### Pipeline Configuration

```bash
pipeline {
    agent any

    tools {
        jdk 'jdk11'
        maven 'maven3'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/malek-jellali/pet-clinic.git'
            }
        }

        stage('Build and Sonar Analysis') {
            steps {
                script {
                    // Build the project
                    sh "mvn clean package"

                    // SonarQube analysis
                    sh "mvn sonar:sonar -Dsonar.host.url=http://172.17.0.1:9001/ \
                        -Dsonar.projectName=pet-clinic \
                        -Dsonar.projectVersion=1.0 \
                        -Dsonar.java.binaries=. \
                        -Dsonar.projectKey=pet-clinic \
                        -Dsonar.login=squ_4451668536d385e57f477fdde6660491c6a51368"
                }
            }
        }
    }
}
```



## Challenges Faced
- Ensuring proper configuration and integration of Jenkins with the Git repository.
- Setting up Docker correctly for containerized builds.
- Configuring the SonarQube analysis for code quality checks.

## Key Takeaways
- **Automation of the CI/CD Pipeline:** Streamlines the software delivery process, reducing manual intervention and improving efficiency.
- **Effective Tool Utilization:** Leveraging tools like Jenkins, Docker, and SonarQube enhances development workflows, ensuring code quality and reliability.
- **Continuous Improvement:** Emphasizing continuous improvement and iteration is crucial for optimizing the CI/CD pipeline and enhancing overall development practices.





