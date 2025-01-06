```
pipeline {
    agent {
        label 'Live-Template'
    }

    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
        GIT_REPO = "https://github.com/Ashadozzaman/Template-Builder.git"
        CLIENT_APP_NAME = "Template-Builder"
        CONFIG_PROJECT_NAME = "template_builder"
        ENV_FILE_PATH = "/var/www/html/env_files/.env" // Stored outside the workspace
        CUSTOM_WORKSPACE = "/var/www/html/template-builder"
        WORKING_WORKSPACE = "/var/www/html/template.workflow.mygov.bd"
    }

    options {
        skipDefaultCheckout(true) // Skips the default checkout to use our custom directory
    }

    stages {
        stage('CLEANUP WORKSPACE') {
            steps {
                script {
                    sh "rm -rf ${CUSTOM_WORKSPACE}/*"
                }
            }
        }

        stage("CHECKOUT GIT REPO") {
            steps {
                dir("${CUSTOM_WORKSPACE}") {
                    checkout([$class: 'GitSCM',
                              branches: [[name: 'main']],
                              userRemoteConfigs: [[url: "${GIT_REPO}", credentialsId: 'Git-Hub-Credential-Template-Ashadozzaman']]
                    ])
                }
            }
        }

        stage("VERIFY CHECKOUT") {
            steps {
                script {
                    sh "ls -la ${CUSTOM_WORKSPACE}"
                }
            }
        }

        stage('Symlink .env') {
            steps {
                script {
                    sh "ln -sf ${ENV_FILE_PATH} ${CUSTOM_WORKSPACE}/.env"
                }
            }
        }

        stage('Restore & Permission') {
            steps {
                echo 'Restoring Backup of env and adjusting permissions'
                sh "chown -R www-data:www-data ${CUSTOM_WORKSPACE}/"
                sh "chmod -R 777 ${CUSTOM_WORKSPACE}/"

                // Set permissions for specific directories
                sh "sudo chown -R www-data:www-data ${CUSTOM_WORKSPACE}/storage ${CUSTOM_WORKSPACE}/bootstrap/cache"
                sh "sudo chmod -R 775 ${CUSTOM_WORKSPACE}/storage ${CUSTOM_WORKSPACE}/bootstrap/cache"
            }
        }

        stage('Update Dependencies') {
            steps {
                dir("${CUSTOM_WORKSPACE}") {
                    // Install Composer dependencies
                    sh 'composer update'
                }
            }
        }

        stage('Database Migration') {
            steps {
                dir("${CUSTOM_WORKSPACE}") {
                    // Perform database-related tasks
                    // sh 'php artisan migrate --force' // Uncomment if you need to run migrations
                    sh 'php artisan cache:clear'
                    sh 'php artisan config:clear'
                    sh 'php artisan optimize:clear'
                }
            }
        }

        stage('Verify Directory After Checkout') {
            steps {
                script {
                    sh 'ls -la /var/www/html'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        success {
            echo 'Pipeline executed successfully.'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }
}

```


## Updated `rsync`
pipeline {
    agent {
        label 'Live-Template'
    }

    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
        GIT_REPO = "https://github.com/Ashadozzaman/Template-Builder.git"
        CLIENT_APP_NAME = "Template-Builder"
        CONFIG_PROJECT_NAME = "template_builder"
        ENV_FILE_PATH = "/var/www/html/env_files/.env" // Stored outside the workspace
        CUSTOM_WORKSPACE = "/var/www/html/template-builder"
        WORKING_WORKSPACE = "/var/www/html/template.workflow.mygov.bd"
    }

    options {
        skipDefaultCheckout(true) // Skips the default checkout to use our custom directory
    }

    stages {
        stage('CLEANUP WORKSPACE') {
            steps {
                script {
                    sh "rm -rf ${CUSTOM_WORKSPACE}/*"
                }
            }
        }

        stage("CHECKOUT GIT REPO") {
            steps {
                dir("${CUSTOM_WORKSPACE}") {
                    checkout([$class: 'GitSCM',
                              branches: [[name: 'main']],
                              userRemoteConfigs: [[url: "${GIT_REPO}", credentialsId: 'Git-Hub-Credential-Template-Ashadozzaman']]
                    ])
                }
            }
        }

        stage("VERIFY CHECKOUT") {
            steps {
                script {
                    sh "ls -la ${CUSTOM_WORKSPACE}"
                }
            }
        }

        stage('Symlink .env') {
            steps {
                script {
                    sh "ln -sf ${ENV_FILE_PATH} ${CUSTOM_WORKSPACE}/.env"
                }
            }
        }

        // Sync Changes Before Running Dependencies & Migrations
        stage('Sync Changes with WORKING_WORKSPACE') {
            steps {
                script {
                    echo "Syncing changes from CUSTOM_WORKSPACE to WORKING_WORKSPACE"
                    // Sync changes using rsync
                    sh "rsync -av --delete ${CUSTOM_WORKSPACE}/ ${WORKING_WORKSPACE}/"
                }
            }
        }

        // Now proceed with Permissions, Composer, Migrations, etc.
        stage('Restore & Permission') {
            steps {
                echo 'Restoring Backup of env and adjusting permissions'
                // Set ownership and permissions for WORKING_WORKSPACE
                sh "chown -R www-data:www-data ${WORKING_WORKSPACE}/"
                sh "chmod -R 777 ${WORKING_WORKSPACE}/"

                // Set permissions for specific directories
                sh "sudo chown -R www-data:www-data ${WORKING_WORKSPACE}/storage ${WORKING_WORKSPACE}/bootstrap/cache"
                sh "sudo chmod -R 775 ${WORKING_WORKSPACE}/storage ${WORKING_WORKSPACE}/bootstrap/cache"
            }
        }

        stage('Update Dependencies') {
            steps {
                dir("${WORKING_WORKSPACE}") {
                    // Install Composer dependencies in the WORKING_WORKSPACE
                    sh 'composer update'
                }
            }
        }

        stage('Database Migration') {
            steps {
                dir("${WORKING_WORKSPACE}") {
                    // Perform database-related tasks in the WORKING_WORKSPACE
                    // sh 'php artisan migrate --force' // Uncomment if you need to run migrations
                    sh 'php artisan cache:clear'
                    sh 'php artisan config:clear'
                    sh 'php artisan optimize:clear'
                }
            }
        }

        stage('Verify Directory After Checkout') {
            steps {
                script {
                    sh 'ls -la /var/www/html'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        success {
            echo 'Pipeline executed successfully.'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }
}
