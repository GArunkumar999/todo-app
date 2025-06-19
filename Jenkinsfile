pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/GArunkumar999/todo-app.git'
            }
        }
        stage('image build'){
            steps{
                script{
                    
                    sh """
                       docker build -t arun596/todoapp:v3 .
                    """
                }
            }
        }
        stage('push to dockerhub'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', passwordVariable: 'pwd', usernameVariable: 'user')]) {
                     sh """
                        docker login -u $user -p $pwd 
                        docker push arun596/todoapp:v3
                        docker rmi arun596/todoapp:v3
                     """
    
                    }
                    
                }
            }
        }
        stage('run image'){
            steps{
                sh 'docker run -d --name TodoApp -p 3000:3000 arun596/todoapp:v3'
            }
        }
    }
    post{
        success{
            echo "build success"
            deleteDir()
        }
        failure{
            echo "build failure"
        }
    }
}