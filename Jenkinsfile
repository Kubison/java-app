pipeline {
    agent any
    environment {
        GITHUB_CREDENTIALS = 'github' // GitHub için eklediğiniz credential'ın ID'si
        K8S_AUTH_KUBECONFIG = credentials('kubeconfig')
}

    

    stages {
        stage('Clone Repository') {
            steps {
                // GitHub kimlik bilgilerini almak için withCredentials kullanılıyor
                withCredentials([usernamePassword(credentialsId: GITHUB_CREDENTIALS, usernameVariable: 'GITHUB_USERNAME', passwordVariable: 'GITHUB_PASSWORD')]) {
                    git branch: 'main',
                        credentialsId: GITHUB_CREDENTIALS,
                        url: 'https://github.com/Kubison/java-app.git'
                }
            }
        }
         stage('Run Ansible Playbook') {
            steps {
            ansiblePlaybook(
                playbook: 'java-app/playbook.yaml', // Ansible playbook dosyanızın yolu
                colorized: true // Opsiyonel, renkli çıktıları etkinleştirir
            )
            }
        }
    }
    
}

