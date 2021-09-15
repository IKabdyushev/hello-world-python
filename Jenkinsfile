pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                git branch: 'dev', url: 'https://github.com/Shkulipa13/hello-world-python.git'
                sh "docker build -t 172.28.1.4:5000/testpython:${BUILD_NUMBER} ."
                sh "docker push 172.28.1.4:5000/testpython:${BUILD_NUMBER}"
            }
        }
        stage('Deploy') {
            steps {
                sh "ansible-playbook -i hosts playbook.yml"
            }
        }
    }
}
