pipeline {
    agent any

    stages {
        stage("Download Resources with Ansible") {
            steps {
                ansiblePlaybook inventory: '/home/smithbriana10gm/OrbitBank/dev.inv', playbook: '/home/smithbriana10gm/OrbitBank/playbook.yml', vaultTmpPath: ''
            }
    }
        stage('Build Frontend Image') {
            steps {
                script {
                    docker.build("frontend:latest", "./frontend")
                }
            }
        }

        stage('Build Backend Image') {
            steps {
                script {
                    docker.build("backend:latest", "./backend")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Assuming you have a Docker daemon running on Jenkins
                    sh 'docker run -d -p 80:80 frontend:latest'
                    sh 'docker run -d -p 3000:3000 backend:latest'
                }
            }
        }
    }
}
