pipeline {
    agent any

    environment {
        TARGET_DIR = "/var/www/html"
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the main branch
                git branch: 'main',
                    url: 'https://github.com/Prabhuccp/FinalsSecureDevOps.git'
            }
        }

        stage('Deploy to Web Server') {
            steps {
                script {
                    sh """
                        echo '🧹 Cleaning old site files...'
                        sudo rm -rf $TARGET_DIR/*

                        echo '📁 Copying new site files...'
                        sudo cp -r * $TARGET_DIR/

                        echo '🔒 Setting permissions...'
                        if id -u apache > /dev/null 2>&1; then
                            sudo chown -R apache:apache $TARGET_DIR
                        else
                            sudo chown -R www-data:www-data $TARGET_DIR
                        fi
                    """
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}
