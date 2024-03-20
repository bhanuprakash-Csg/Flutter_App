pipeline {

    agent any

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [['https://github.com/bhanuprakash-Csg/Flutter_App.git']]
                ])
            }
        }
        stage('Adding dependencies') {
            steps {
                sh 'flutter pub get' // Example build command
                sh 'flutter pub upgrade'
            }
        }
        stage('Build') {
            steps {
                sh 'flutter clean' // Example test command
                sh 'flutter build web'
            }
        }
       

        stage('Build Deploy Code') {
            when {
                branch 'feature1'
            }
            steps {
                sh 'flutter pub get' // Example build command
                sh 'flutter pub upgrade'
                sh 'flutter clean'
                sh 'flutter build web' 
            }
        }

    }   
}
