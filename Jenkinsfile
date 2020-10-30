
pipeline {
    agent any
    
    environment {
        DB_PASSWORD=credentials('DATABASE_PASSWORD')
    }
    stages {  
        stage('Install Docker and Docker-compose') {
            steps {
            sh 'curl https://get.docker.com | sudo bash'
            sh 'sudo usermod -aG docker jenkins'
            sh 'sudo apt-get update'
            sh 'sudo apt install -y curl jq'
            sh 'sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose'
            sh 'sudo chmod +x /usr/local/bin/docker-compose'
            }
        }
        
        stage('Deploy app') {
            steps {
            sh 'sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d'
            }
        }
        
        stage('Show password') {
            steps {
                sh "echo ${DB_PASSWORD}"
        }
            
    }       
}
