pipeline {
    agent any
    environment {
        REMOTE_SERVER = 'root@awaisinstance-20240521-055418'
        REMOTE_ZONE = 'us-central1-c'
        REMOTE_PATH = '/var/www/html'
       CREDENTIALS_ID = '786a12b456c738dd6a37a28c9687fff6d7e8d5db'  // Replace with your credentials ID
    }
    stages {
        stage('Build') {
            steps {
                echo 'Application build stage...'
            }
        }
        stage('Test') {
            steps {
                withCredentials([file(credentialsId: CREDENTIALS_ID, variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
                    sh 'pwd'
                    sh 'ls -la ${WORKSPACE}'
                    sh 'gcloud auth activate-service-account --key-file=$GOOGLE_APPLICATION_CREDENTIALS'
                    sh 'gcloud compute ssh ${REMOTE_SERVER} --zone=${REMOTE_ZONE} -- "rm -rf ${REMOTE_PATH}/*"'
                    sh 'gcloud compute scp --recurse ${WORKSPACE}/* ${REMOTE_SERVER}:${REMOTE_PATH} --zone=${REMOTE_ZONE}'
                }
            }
        }
        stage('Run') {
            steps {
                echo 'Application run stage'
            }
        }
    }
}
