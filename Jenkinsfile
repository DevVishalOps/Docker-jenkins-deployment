pipeline {
    agent any
    stages {
        stage("Checkout") {
            steps {
                checkout scm
            }
        }

        stage("Test") {
            steps {
                script {
                    // Install npm
                    sh 'sudo apt update'
                    sh 'sudo apt install npm -y'
                    // Run npm test
                    sh 'npm test'
                }
            }
        }

        stage("Build") {
            steps {
                script {
                    // Run npm build
                    sh 'npm run build'
                }
            }
        }
    }
}
