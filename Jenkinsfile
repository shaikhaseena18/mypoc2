pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git credentialsId: 'git-cred',
                    url: 'https://github.com/shaikhaseena18/mypoc2.git',
                    branch: 'main'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t my-java-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop my-java-app || true
                docker rm my-java-app || true
                docker run -d --name my-java-app my-java-app
                '''
            }
        }
    }
}
