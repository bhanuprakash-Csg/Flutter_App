pipeline {

    options {
        buildDiscarder(logRotator( 
            daysToKeepStr: '16', 
            numToKeepStr: '10'
        ))
    }

    agent any

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                echo "Cleaned Up Workspace For Project"
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/bhanuprakash-Csg/Flutter_App.git']]
                ])
            }
        }

        stage('Unit Testing') {
            steps {
                echo "Running Unit Tests"
                // Add your unit testing commands here
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Running Code Analysis"
                // Add your code analysis commands here
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                echo "Building Artifact"
                // Add your build commands here

                echo "Deploying Code"
                // Add your deployment commands here
            }
        }

    }   
}
