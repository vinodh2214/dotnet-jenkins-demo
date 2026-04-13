pipeline {
    agent any

    tools {
        // Make sure .NET SDK is configured in Jenkins
        // name should match Jenkins global tool config
        dotnetsdk 'dotnet6' 
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/vinodh2214/dotnet-jenkins-demo.git'
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            steps {
                sh 'dotnet test --logger "trx;LogFileName=test_results.trx"'
            }
        }
    }

    post {
        always {
            // Publish test results in Jenkins
            junit '**/*.trx'
        }

        success {
            echo 'All tests passed ✅'
        }

        unstable {
            echo 'Some tests failed ⚠️'
        }

        failure {
            echo 'Build failed ❌'
        }
    }
}
