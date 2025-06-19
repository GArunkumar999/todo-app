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
                       docker build -t todoapp:latest .
                    """
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