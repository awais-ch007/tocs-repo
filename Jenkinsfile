
              
     
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
                // Add your test stage steps here
            }
        }
        stage('Run') {
            steps {
                // Add your run stage steps here
            }
        }
    }
}
