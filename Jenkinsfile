pipeline {
    agent any

    environment {
        ENV = "dev"
        APP_NAME = "sample-app"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/tejanaveengit/Ansibledemo.git'
            }
        }

        stage('Build') {
            steps {
                dir('app') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Deploy using Ansible') {
            steps {
                sh """
                ansible-playbook ansible/deploy.yml \
                  -i ansible/inventory/${ENV} \
                  -e app_name=${APP_NAME}
                """
            }
        }
    }

    post {
        success {
            echo "✅ Deployment completed successfully"
        }
        failure {
            echo "❌ Deployment failed"
        }
    }
}
