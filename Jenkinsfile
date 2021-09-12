pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                git branch: 'master', url: 'https://github.com/Shkulipa13/hello-world-python.git'
                sh "docker build -t localhost:8080/${BUILD_NUMBER} ."
                sh 'docker-compose up -d'
            }
        }
    }
}
