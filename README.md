# Docker-jenkins-deployment-Project

Deployment of App on docker using jenkins pipeline and pushing the image to dockerhub

## Steps

1.clone this public get repository in your jenkins server
```bash
git clone https://github.com/DevVishalOps/Student-jenkins-pipeline-Project.git
#this is groovy script repository 
```

2.Create pipline using below steps
    
- Go jenkins dashboard ------> 
- new item --------> 
- select pipline as code--> 
- Select pipeline ------> 
- pipeline script from SCM-->
- select GIT ---> 
- Enter Groovy script url mentioned above --> 
- choose branch according--> 
- Script path Enter name of Groovy script File

```bash
pipeline {
    agent any
    stages{
        stage("checkout"){
            steps{
                checkout scm
            }
        }

        stage("Test"){
            steps{
                sh 'sudo apt install npm'
                sh 'npm test'
            }
        }        
        stage("Build"){
            steps{
                sh 'npm run build'
            }
        }

        stage("Build Image"){
            steps{
                sh 'docker build -t my-node-app:1.0 .'
            }
        } 

          stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_cred', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                    sh "docker tag my-node-app:1.0 vishalrajput0502/my-node-app:1.0"
                    sh "docker push vishalrajput0502/my-node-app:1.0"
                    sh "docker logout"
                }
            }
        }
        
    }
}
```


 - You need to add your dockerhub credentials in jenkins credtenails and make changes in above pipeline .

- If pipeline is build successfully then it should be push my-node-app image  to your dockerhub
