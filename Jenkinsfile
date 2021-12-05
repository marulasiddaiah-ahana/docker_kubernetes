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
                sh 'ls'
                echo = "docker build -t ahanasystems/react-test -f ./client/Dockerfile.dev ./client"
                sh 'docker build -t ahanasystems/react-test -f ./client/Dockerfile.dev ./client'
            
            }
        }

        stage('Test') {
            steps {
                sh 'docker run ahanasystems/react-test npm test -- --coverage'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t ahanasystems/multi-client ./client'
                sh 'docker build -t ahanasystems/mult-nginx ./nginx'
                sh 'docker build -t ahanasystems/multi-server ./server'
                sh 'docker build -t ahanasystems/multi-worker ./worker'
            }
        }
    
    
        stage('Push Images to Docker Hub') {
            steps {
                sh 'docker login -u ahanasystems -p Siddaiah@1994'
                sh 'docker push ahanasystems/multi-client'
                sh 'docker push ahanasystems/mult-nginx'
                sh 'docker push ahanasystems/multi-server'
                sh 'docker push ahanasystems/multi-worker'
            }
        }
    }
}