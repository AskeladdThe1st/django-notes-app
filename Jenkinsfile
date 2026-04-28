@Library("shared") _
pipeline {
    
    agent { label "yusuf" }
    stages {
        stage('Hello') {
            steps{
                script {
                    hello()
                }
            }
        }
        
        stage('Code') {
            steps{
                scripts {
                    clone("https://github.com/LondheShubham153/django-notes-app.git", "dev")
                }
            }
        }
        stage('Build') {
            steps{
                scripts{
                    docker_build("notes-app", "latest", "flokiflopped"
                }
            }
        }
        stage('Pushing image to DockerHub') {
            steps{
                script{
                    docker_push("notes-app", "latest", "flokiflopped")
                }
            }
        }
        stage('Deploy') {
            steps{
                echo "Deploying Code"
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}
