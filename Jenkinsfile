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
                       docker build -t arun596/todoapp:v2 .
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
                        docker push arun596/todoapp:v2
                        docker rmi arun596/todoapp:v2
                     """
    
                    }
                    
                }
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