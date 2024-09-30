pipeline {
    agent any
    
    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/Syedoaun/MLOPS_TASK_3.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("mlops_task3")
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                script {
                    // Run the test script inside the built Docker image
                    docker.image("mlops_task3").inside {
                        sh 'python test_app.py'  
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying...'
                    // Example Docker run command for deployment
                    // Replace with your actual deployment configuration and port mapping
                    sh 'docker run -d -p 8080:8080 mlops_task3'
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
