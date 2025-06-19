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
                       docker build -t arun596/todoapp:v1 .
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
                        docker push arun596/todoapp:v1
                        docker rmi arun596/todoapp:v1
                     """
    
                    }
                    
                }
            }
        }
    }
    post{
        success{
            echo "build success"
        }
        failure{
            echo "build failure"
        }
    }
}