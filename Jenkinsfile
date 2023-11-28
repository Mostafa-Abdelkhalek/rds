pipeline {
    agent {
        label 'ec2-bastion'
    }
    stages {
        stage('preparation') {
            steps {
                git 'https://github.com/Mostafa-Abdelkhalek/rds.git'
            }
        }
        stage('build') {
            steps {
                withCredentials([usernamePassword(credentialsId: "test", usernameVariable: "username", passwordVariable: "pass")]) {
                    sh 'docker build . -t tataimage'
                    sh 'docker login -u ${username} -p ${pass}'
                    sh 'docker push tataimage'
                }
            }
        }
        stage('deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: "test", usernameVariable: "username", passwordVariable: "pass")]) {
                    sh 'docker run -d -p 3000:3000 -t tataimage'
                }
            }
        }
    }
}
