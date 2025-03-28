pipeline {
    agent any

    environment {}

    stages {
        stage('Build and Start LocalStack Container') {
            steps {
                script {
                    // Build with both latest and build-specific tags
                    sh "docker compose up -d"
                }
            }
        }
        stage('Run Terraform Init and Validation') {
            steps {
                script {
                    ssh '''
                        terraform init
                        terraform validate
                        terraform fmt --recursive --check
                        terraform plan
                        terraform show
                    '''
                }
            }

        }
    }

    post {
        always {
            // Clean up workspace
            cleanWs()
        }
    }
}
