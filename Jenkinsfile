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
                // Remove existing files on the remote server first
                sh '''
                    gcloud compute ssh root@awaisinstance-20240521-055418 --zone=us-central1-c -- "rm -rf /var/www/html/*"
                '''
                // Then copy new files from Jenkins workspace to the remote server
                sh '''
                    gcloud compute scp --recurse /var/lib/jenkins/workspace/Dev-Op-Project_main/* root@awaisinstance-20240521-055418:/var/www/html --zone=us-central1-c
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
