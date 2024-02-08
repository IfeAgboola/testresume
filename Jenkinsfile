pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET = 'jenkinsbife'
        GITHUB_REPO_URL = 'https://github.com/IfeAgboola/testresume.git'
        GITHUB_BRANCH = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: "${env.GITHUB_BRANCH}", url: "${env.GITHUB_REPO_URL}"
                }
            }
        }

        stage('Upload to S3') {
            steps {
                script {
                    sh "aws s3 sync . s3://${env.S3_BUCKET}/path/to/store/files --delete --exclude '.git/*'"
                }
            }
        }
    }

    post {
        success {
            echo 'Files successfully uploaded to S3!'
        }
        failure {
            echo 'Failed to upload files to S3.'
        }
    }
}
