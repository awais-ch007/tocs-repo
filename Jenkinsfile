pipeline {
   agent any
    environment {
        PROJECT_ID = 'devops-project-423307'
        SERVICE_ACCOUNT_KEY = credentials('786a12b456c738dd6a37a28c9687fff6d7e8d5db')
    stages {
        stage('Build') {
            steps {
                echo 'Application build stage...'
            }
        }
        stage('Test') {
            steps {
                // Print the current working directory
                sh 'pwd'
                
                // List the contents of the Jenkins workspace
                sh 'ls -la ${WORKSPACE}'

                // Remove existing files on the remote server first
               
               sh """
                    gcloud auth activate-service-account --key-file=${SERVICE_ACCOUNT_KEY}
                    gcloud config set project ${PROJECT_ID}
                    gcloud config set compute/zone us-central1-c
                    gcloud compute ssh root@awaisinstance-20240521-055418 -- rm -rf /var/www/html/*
                """
            

                // Then copy new files from Jenkins workspace to the remote server
                sh '''
                    gcloud compute scp --recurse ${WORKSPACE}/* root@awaisinstance-20240521-055418:/var/www/html --zone=us-central1-c
                '''
            }
        }
        stage('Run') {
            steps {
                echo 'Application run stage'
            }
        }
    }
}
