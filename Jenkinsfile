pipeline {
    agent any
    tools {nodejs "Node_20"}
    stages {
        stage('Build') {
            steps {
                echo 'Pipeline build started...'
		dir('./react-tetris'){
			sh 'git pull origin master'
			sh 'npm install'
			sh 'npm run build'
		}
		
            }
            post {
                success {
                    echo 'SUCCESS'
                }
                failure {
                    echo 'FAIL'
		    mail to: "luczak.roza@gmail.com",
		    subject: "Pipeline failed",
                    body: "Pipeline build failed."
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Pipeline testing started...'
		dir('./react-tetris'){
                	sh 'npm test'
		}
            }
            post {
                success {
                    echo 'SUCCESS'
                }
                failure {
                    echo 'FAIL'
		    mail to: "luczak.roza@gmail.com",
		    subject: "Pipeline failed",
                    body: "Pipeline tests failed."
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
		    mail to: "luczak.roza@gmail.com",
		    subject: "Pipeline failed",
                    body: "Pipeline deploy failed."
                }
            }
        }
    }
}