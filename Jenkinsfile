pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet restore'
                    } else {
                        bat 'dotnet restore'
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet build --no-restore'
                    } else {
                        bat 'dotnet build --no-restore'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet test --logger "trx;LogFileName=test_results.trx"'
                    } else {
                        bat 'dotnet test --logger "junit;LogFilePath=test-results.xml"'
                    }
                }
            }
        }
    }

   post {
    always {
        junit '**/test-results.xml'
    }
}
}
