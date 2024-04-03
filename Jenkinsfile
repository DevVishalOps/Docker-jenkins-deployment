pipeline {
    agent any
    stages {
        stage("checkout") {
            steps {
                checkout scm
            }
        }
        stage("Test") {
            steps {
                script {
                    sh 'sudo apt update -y && sudo apt install npm -y'
                    sh 'npm test'
                }
            }
        }        
        stage("Build") {
            steps {
                sh 'npm run build'
            }
        }
    }
}
