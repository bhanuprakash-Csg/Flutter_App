pipeline {
    agent any
    
    options {
        buildDiscarder(logRotator( 
            daysToKeepStr: '16', 
            numToKeepStr: '10'
        ))
    }

    triggers {
        githubPullRequest {
            adminUsers('your-github-username') // Replace 'your-github-username' with your actual GitHub username
            branchFilterType('All')
            branchesFilter {
                pattern('feature1') // Trigger only for pull requests against the 'feature1' branch
            }
        }
    }

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
            
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Running Code Analysis"
               
            }
        }

        stage('Build Deploy Code') {
            when {
                expression { env.CHANGE_TARGET == 'feature1' } // Execute only when the target branch of the PR is 'feature1'
            }
            steps {
                echo "Building Artifact"
              

                echo "Deploying Code"
              
            }
        }

    }   
}
