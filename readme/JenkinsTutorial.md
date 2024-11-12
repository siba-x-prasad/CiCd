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

## Github Jenkins
- In this case, we will provide the github link and it will
- Steps
- Create your own Maven project or clone it from somewhere
- Create a Jenkins file and write the stages like above
- I am using this repo https://github.com/siba-x-prasad/jenkins-aws-java-maven-app-Swasi.git
- You will find the JenkinsFile here : https://github.com/siba-x-prasad/jenkins-aws-java-maven-app-Swasi/tree/main/jenkinsfiles
- Now open localhost/8080
- Create new Item
- Select PipeLine
- Enter name of the pieline
- under Pipeline section
  - select ```Pipeline script from SCM```
  - SCM : select git
  - Repository URL : use your repository
  - Credential if it's a private repository, for public repository, no credential require
  - Select the branch you want to proceed with (In this case main branch)
  - Script Path : path of the JenkinsFile
- Click save, then build the 
## Polling SCM (How to get latest coe from Github)
- Got to pipeline in Jenkins
- select configure
- Go to Build Trigger Section
- Select Poll SCM
- For time visit : https://crontab.guru
- In my case, it will run after 2 minutes - ```H/2 * * * *```
- That means, If any changes occur in Github, after 2 minutes, it will trigger Jenkins build
- We don't need to trigger the Jenkins Build
- It will automatically trigger the build 2 minutes after commit.

## Multi Branch Pipe Line
- Create New Item
- Enter Pipe Line
- Select MultiBranch Pipeline
- Now Select Git
- Enter the repository
- It will fetch all the branches
- Then enter the path of the Jenkins files in each branch
- Make sure all have the same path
- Set the time as 2 minutes
- Once you save it, it will start building for the number of branch u have
- If there are 3 branches, then 3 Build Pipe line will run parallelly.
## Parameterized Pipeline
## Boolean parameter
```
pipeline {
  agent any
  parameters {
    booleanParam(defaultValue: false, description: "Enable Service?", name:"myBoolean")
  }
 
  stages {
    stage("Boolean Parameter Demo"){
        steps {
            echo "booleanParam is set to : ${params.myBoolean}"
        }
    }   
  }
}
```
## String Param
```
pipeline {
  agent any
  
  parameters {
    string(defaultValue: "TEST", description: "Which Environment to deploy", name:"deployEnv")
  }

  stages {
    stage("String Parameter Demo"){
        steps {
            echo "Which Environment to deplay : ${params.deployEnv}"
        }
    }
  }
}
```
## Multiple Choice
```
pipeline {
  agent any
  parameters {
    choice(choices: ["TEST", "DEV", "QA", "PRE-PROD"], description: "Which Environment to deploy", name:"deployEnv")
  }

  stages {
    stage("Boolean Parameter Demo"){
        steps {
            echo "Choice is set to : ${params.deployEnv}"
        }
    }
  }
}
```
- Got to dashboard
- ![CI](https://github.com/siba-x-prasad/CiCd/blob/main/images/multipleChoiceParam.png)
- ![CI](https://github.com/siba-x-prasad/CiCd/blob/main/images/selectMultipleChoiceBuild.png)
## Choice with confirmation checkbox
```
pipeline {
  agent any
  parameters {
    string(defaultValue: "", description: "Deployment Name?", name: "deploymentName")
    choice(choices: ["TEST", "DEV", "QA", "PRE-PROD"], description: "Which Environment to deploy", name:"deployEnv")
    booleanParam(defaultValue: false, description: "Confirm Deployment", name: "confirmDeployment")
  }

  stages {
    stage("Boolean Parameter Demo"){
        steps {
            echo "Deployment Name set to : ${params.deploymentName} \n"
            echo "Choice is set to : ${params.deployEnv} \n"
            echo "bool is set to : ${params.confirmDeployment} \n"
        }
    }
  }
}
```
- Got to dashboard
- ![CI](https://github.com/siba-x-prasad/CiCd/blob/main/images/multipleChoiceParam.png)
- ![CI](https://github.com/siba-x-prasad/CiCd/blob/main/images/selectMultipleChoiceBuild.png)
- ![CI](https://github.com/siba-x-prasad/CiCd/blob/main/images/challenge3.png)
- In Console output u will see the values u printed above.
## Jenkins Variable
- In Jenkins Pipelines, a variable is a symbolic name that represents data that can change dynamically during the execution of the pipeline. 
- Variables are essential for managing configuration settings, storing data, and controlling the behavior of your pipeline scripts.
- **Environment Variables:** 
  - These are key-value pairs available to the Jenkins environment and can be accessed within your pipeline script. 
  - They usually include system-specific configurations or user-defined variables. 
  - Access them using env.VARIABLE_NAME.
- Example
```
pipeline {
  agent any
  
  environment {
    def myString = "Hello World"
    def myNumber = 10
    def myBool = true
  }

  stages {
    stage("Boolean Parameter Demo"){
        steps {
            echo "myString : ${myString} \n"
            echo "myNumber : ${myNumber} \n"
            echo "myBool : ${myBool} \n"
        }
    }
  }
}
```
## Jenkins Specific Environment Variable
- [Visit here] (https://www.jenkins.io/doc/book/pipeline/jenkinsfile/)
- Search for BUILD_NUMBER
- ```
  echo "Current workspace: ${env.WORKSPACE}"
  echo "BUILD NUMBER: ${env.BUILD_NUMBER}"
  ```
## Advance Jenkins
- In background jenkins uses groovy as a language
- Learn the basic of groovy [here] (https://groovy-lang.org/documentation.html#gettingstarted)
- To write complex pipeline logic, you need groovy
## Build Health
- **Sunshine:** All builds are successful
- **Cloudy:** some of the builds are successful
- **Raining:** all builds are failing
## Credential
- follow for more : https://www.jenkins.io/doc/book/using/using-credentials/

## JenkinsFile name

## Multiple Jenkins Files
- You can have multiple different jenkins files in a project.
- every files have different purpose

## Debug
- use ```sleep(10)``` to halt the buld process for 10 seconds
```
pipeline {
  agent any
  
  environment {
    def myString = "Hello World"
    def myNumber = 10
    def myBool = true
  }

  stages {
    stage("Boolean Parameter Demo"){
        steps {
            echo "myString : ${myString} \n"
            echo "myNumber : ${myNumber} \n"
            echo "myBool : ${myBool} \n"
            sleep(20)
            echo "Current workspace: ${env.WORKSPACE}"
            echo "BUILD NUMBER: ${env.BUILD_NUMBER}"
        }
    }
  }
}
```
## if statement
```
pipeline {
  agent any
  parameters {
    booleanParam(defaultValue: false, description: "enableService ?", name: "isServiceEnable")
  }

  stages {
    stage("If statement demo"){
       steps {
          script {
              if(params.isServiceEnable == false) {
                currentBuild.result = "SUCCESS"
                return
              } 
              else {
                echo "isServiceEnable set to : TRUE"
              }
          }
       }
    }
  }
}
```
## Function
- In jenkins use function if you want to perform some action multiple times.
```
pipeline {
  agent any

  stages {
    stage("Demo"){
       steps {
          myFunc("Sibaprasad")
          myFunc("abcd")
       }
    }
  }
}

def myFunc(String myText) {
    echo "NAME is ${myText} \n"
}
```
## Variable Scope
```
pipeline {
  agent any

environment {
  def name = "Sibaprasad"
}
  stages {
    stage("Demo"){
       steps {
          myFunc("Sibaprasad")
          myFunc("abcd")
       }
    }
  }
}

def myFunc(String myText) {
    def localName = "abcd"
    echo "NAME is ${myText} \n"
}
```
- above name variable is global
- localName is local to function only
