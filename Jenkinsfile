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
                sh 'sudo apt update'
                sh 'sudo apt install npm -y'
                sh 'sudo npm test'
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
    }
}
