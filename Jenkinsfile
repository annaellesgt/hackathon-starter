pipeline {
    agent {
        docker {
            image 'node:8-slim' 
            args '-p 8080:8080'
        }
    }

    stages {
        stage('Dev') {
            steps {
                sh 'echo "Bulding in develop"'
                sh 'npm install' 
                sh 'npm run' 
            }
        }
    stage('Preprod') {
        steps {
            sh 'echo "Bulding in preprod"'
            sh 'make check || true'
            cypress '**/target/*.xml'
        }
    }
    stage('Prod') {
        steps {
            sh 'echo "Bulding in prod"'
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS' (1)
                }
            }
            steps {
                sh 'make publish'
            }
        }
    }
    }
}