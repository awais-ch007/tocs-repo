pipeline {
    agent any

    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout scm: [$class: 'GitSCM', branches: [[name: 'AI']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/awais-ch007/tocs-repo.git']]]
            }
        }
        stage('Build') {
            steps {
                echo 'Application build stage...'
            }
        }
        stage('Test') {
            steps {
                sh 'pwd'
                sh 'ls -la'
                withCredentials([usernamePassword(credentialsId: 'gcloud-credentials', passwordVariable: 'GCLOUD_PASSWORD', usernameVariable: 'GCLOUD_USERNAME')]) {
                    sh """
                        gcloud auth activate-service-account --key-file=/var/lib/jenkins/workspace/Tocs-proj_AI/gcloud-credentials.json
                        gcloud compute ssh root@awaisinstance-20240521-055418 --zone=us-central1-c -- rm -rf /var/www/html/*
                    """
                }
            }
        }
        stage('Run') {
            steps {
                // Add your run stage steps here
            }
        }
    }
}
