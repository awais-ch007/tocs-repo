pipeline {
    agent any
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
                    gcloud auth default --scopes=https://www.googleapis.com/auth/compute,https://www.googleapis.com/auth/cloud-platform
                    gcloud compute ssh root@awaisinstance-20240521-055418 --zone=us-central1-c -- rm -rf /var/www/html/*
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
