pipeline {
    agent {
        docker {
            image 'maven:3.8.1-jdk-8'
            args '-v /tmp:/tmp'
        }
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker stop flask-app || true'
                sh 'docker rm flask-app || true'
                sh 'docker run -d --name flask-app -p 8000:8000 flask-app'
            }
        }
    }
    
    post {
        always {
            sh 'docker image prune -f'
        }
    }
}
