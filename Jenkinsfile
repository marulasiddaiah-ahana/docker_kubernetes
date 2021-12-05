pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Digital Registers Deployment Automation'
                checkout scm
            }
        }
    
    
        stage('Before Install') {
            steps {
                bat 'docker build -t ahanasystems/react-test -f ./client/Dockerfile.dev ./client'
            
            }
        }

        stage('Test') {
            steps {
                bat 'docker run ahanasystems/react-test npm test -- --coverage'
            }
        }

        stage('Build') {
            steps {
                bat 'docker build -t ahanasystems/multi-client ./client'
                bat 'docker build -t ahanasystems/mult-nginx ./nginx'
                bat 'docker build -t ahanasystems/multi-server ./server'
                bat 'docker build -t ahanasystems/multi-worker ./worker'
            }
        }
    
    
        stage('Push Images to Docker Hub') {
            steps {
                bat 'docker login -u ahanasystems -p Siddaiah@1994'
                bat 'docker push ahanasystems/multi-client'
                bat 'docker push ahanasystems/mult-nginx'
                bat 'docker push ahanasystems/multi-server'
                bat 'docker push ahanasystems/multi-worker'
            }
        }
    }
}