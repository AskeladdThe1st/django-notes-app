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
                echo "Cloning Code"
                git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "dev"
                echo "Code has been successfully cloned!"
            }
        }
        stage('Build') {
            steps{
                echo "Building the code retrieved from github"
                sh "docker build -t notes-app:latest ."
            }
        }
        stage('Pushing image to DockerHub') {
            steps{
                withCredentials([usernamePassword('credentialsId':"dockerhub-credentials",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
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
