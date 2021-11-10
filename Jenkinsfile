pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Prepare environments') {
            steps {
                withCredentials([string(credentialsId: 'myssh', variable: 'SSH_PASSWORD')]) {
                  sh "ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts playbook.yml -e ansible_password=${SSH_PASSWORD} -e ansible_sudo_pass=${SSH_PASSWORD}"
                }
            }
        }
        stage('Build') {
            steps {
                sh "docker build -t 172.28.1.4:5000/testpython:${BUILD_NUMBER} ."
                sh "docker push 172.28.1.4:5000/testpython:${BUILD_NUMBER}"
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([string(credentialsId: 'myssh', variable: 'SSH_PASSWORD')]) {
                  sh "DOCKERANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts deploy.yml -e ansible_password=${SSH_PASSWORD} -e BUILD_NUMBER=${BUILD_NUMBER}"
                }
            }
        }
    }
}
