pipeline{
    agent any
    stages{
        stage("Code"){
            steps{
                echo "Cloning the code"
                git url:"https://github.com/yadavparth6393/django-notes-app.git", branch: "main"
            }
            
        }
        
        stage("build"){
            steps{
                echo "Building the code"
                sh "docker build -t my-notes-app ."
            }
            
        }
        stage("Push to docker hub"){
            steps{
                echo "Push the image to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubpass",usernameVariable:"dockerhubuser")]){
                sh "docker tag my-notes-app ${env.dockerhubuser}/my-notes-app:latest" 
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass} "
                sh "docker push ${env.dockerhubuser}/my-notes-app:latest"
                    }
            }
            
        }
        stage("Deploy"){
            steps{
                echo "Deploying the container"
                sh "docker run -d -p 8000:8000 parth6393/my-notes-app:latest "
                
            }
            
        }
        
    }
    
    
    
}
