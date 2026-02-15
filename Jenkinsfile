@Library("Shared") _
pipeline{
    agent {label "agent-1"}
    
    stages{
        stage("Code"){
            steps{
                script{
                    clone("https://github.com/Pratik1805/django-notes-app.git","main")
                }
            }
        }
        stage("Build"){
            steps{
                script{
                    docker_build("jsilverhand18","notes-app","latest")
                }
            }
        }
        stage("Test"){
            steps{
                echo  "This is Testing the code"
            }
        }
        stage("Push to DockerHub"){
            steps{
                script{
                    docker_push("notes-app","latest","jsilverhand18")
                }
            }
        }
        stage("Deploy"){
            steps{
                echo  "This is Deploying the code"
                sh "docker compose up -d"
                echo "Deploying done"
            }
        }
    }
 post {
        success {
            echo "Deployment successful!"
        }
        always {
            // Clean up only 'dangling' images to keep the build fast
            sh 'docker image prune -f'
        }
    }
    
}
