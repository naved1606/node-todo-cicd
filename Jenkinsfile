pipeline {
    
    agent { label'dev-agent' }

    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/naved1606/node-todo-cicd.git', branch:'master'
                
            }
            
        }
        stage('Build and test'){
            steps{
                sh 'docker build . -t naved1606/node-todo-app:latest'
                
            }
            
        }
        stage('login to docker & push image'){
            steps{
                echo 'logging to dockerhub and pushing image'
                withCredentials([usernamePassword(credentialsId:'dockerHub', passwordVariable:'dockerHubPswd', usernameVariable:'dockerHubUser')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPswd}"
                    sh "docker push naved1606/node-todo-app:latest"
                }
            }
            
        }
        stage('Deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
                
            }
            
        }
    }
    
    
    
}
