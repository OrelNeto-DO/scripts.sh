pipeline {
    agent any
    
    triggers {
        pollSCM('* * * * *')  
    }
    
    stages {
        stage('Cleanup') {
            steps {
                echo "Cleaning up workspace..."
                sh 'rm -rf *'
            }
        }

        stage('Clone') {
            steps {
                echo "Cloning repository..."
                sh "git clone https://github.com/OrelNeto-DO/devops-course.git"
            }
        }

        stage('Copy ENV') {
            steps {
                dir('devops-course/docker_projects/exercise_flask_with_mySQL') {
                    echo "Copying .env file from local machine..."
                    sh "cp /home/orelnetodo/Desktop/flask_mysql_env .env"
                }
            }
        }

        stage('Build') {
            steps {
                dir('devops-course/docker_projects/exercise_flask_with_mySQL') {
                    echo "Building application..."
                    sh '''
                        docker-compose down || true
                        docker-compose up -d
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                dir('devops-course/docker_projects/exercise_flask_with_mySQL') {
                    echo "Testing application..."
                    sh 'sleep 10'  // להמתין לפני הבדיקה
                    sh 'curl -f http://192.168.187.128:5005'
                }
            }
        }
    }
}
