# Jenkins Tutorial - Udemy
## Create Jenkins Job using Docker
## Important Links
- [Jenkins Basic Pipeline steps] (https://www.jenkins.io/doc/pipeline/steps/workflow-basic-steps/)
- [Jenkins Pipeline Syntax] (https://www.jenkins.io/doc/book/pipeline/syntax/)

- After docker set up and it generate the password using the below command
- ```docker run -p 8080:8080 -p 50000:50000 --restart=on-failure jenkins/jenkins:lts-jdk17```
- Now click open browse : localhost:8080
- Continue as admin
- Click on create Job
- it will show different types of job
- ![CI](https://github.com/siba-x-prasad/CiCd/blob/main/images/jenkinsJobtype.png)
- Select Freestyle
- Then click okay.
- Scroll down
- Under Build
- click on add Build step
- select execute shell
- type inside command - echo "Hello My first Job"
- Click Save
- Click build now from the left menu
- ![CI](https://github.com/siba-x-prasad/CiCd/blob/main/images/Jenkins_udemy_build1.png)
- In console log, u will see Hello My First Job
## Maven set up
- https://github.com/jenkins-docs/simple-java-maven-app
- Open visual studio code
- Create a folder
- Create a file name - Jenkinsfile
- Open Jenkins - localhost:8080
- Go to dashboard
- Click on new Item
- Select Pipeline
- Click ok
- Go to pipeline script :  where we will write pipeline script
- Under Build trigger
## Build Triggers
 - Build after other projects are built
- Build periodically
- GitHub hook trigger for GITScm polling
- Poll SCM - It will fetch the SCM from repository, github, bitbucket if any changes made
- Quiet period
- Trigger builds remotely (e.g., from scripts)

## How to check the details of the docker container
- open command line
- type : ```docker container ls```
- Make sure that docker is running
- now type the below command with docker id
- docker exec -it -u root container_id /bin/bash
- ```docker exec -it -u root 523a44110385 /bin/bash```
-  Now it will open a command line
- #root@523a44110385: (roo@container_id)
- run - ```apt-get update```
- To install maven: ```apt-get install maven```
## Pipeline statement
- Now open the jenkinsfile in vscode (under JenkinsMavenSetup)

## Jenkinsfile
```
pipeline {
  agent any
  sgates {
    stage("Clean Up"){
        steps {
            deleteDir()
        }
    }   
    stage("Clone Repo"){
        steps {
            sh "git clone https://github.com/jenkins-docs/simple-java-maven-app.git"
        }
    }
    stage("Build"){
        steps {
           dir("simple-java-maven-app"){
              sh "mvn clean install"
           }
        }
    }
    stage("Test"){
        steps {
           dir("simple-java-maven-app"){
              sh "mvn test"
           }
        }
    }
  }
}
```
## stage("Clean Up")
- In this stage, it will cleanup by deleting the directory, so that it will not make any issue is previous build have any error
##  stage("Clone Repo")
- It will clone the repository
## stage("Build")
- It will build the application by installing the libs from maven from star
## stage("Test")
- It will test

## Now add pipeline script to jenkins
- paste the above code block inside the pipeline script
- Save
- Start Build
- 