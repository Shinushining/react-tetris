pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Pipeline build started...'
		sh 'npm install'
		sh 'npm run build'
            }
            post {
                success {
                    echo 'SUCCESS'
                }
                failure {
                    echo 'FAIL'
                    emailext body: "Pipeline build failed.",
                                     subject: "Pipeline failed",
                                     to: "luczak.roza@gmail.com"
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Pipeline testing started...'
                sh 'npm test'
            }
            post {
                success {
                    echo 'SUCCESS'
                }
                failure {
                    echo 'FAIL'
                    emailext body: "Pipeline tests failed.",
                                     subject: "Pipeline failed",
                                     to: "luczak.roza@gmail.com"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Pipeline deployment started...'
                sh 'docker-compose up --detach'
            }
            post {
                success {
                    echo 'SUCCESS'
                }
                failure {
                    echo 'FAIL'
                    emailext body: "Pipeline deploy failed.",
                                     subject: "Pipeline failed",
                                     to: "luczak.roza@gmail.com"
                }
            }
        }
    }
}