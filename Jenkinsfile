pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                 checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/bhanuprakash-Csg/Flutter_App.git']]
                ])
            }
        }

        stage('Build and Test') {
            steps {
                // Your build and test steps go here
                // For example:
                echo'npm install'
                echo 'npm test'
            }
        }

        stage('Deploy') {
            when {
                // Only deploy if the PR is from feature1 to main
                expression {
                    return env.CHANGE_TARGET == 'main' && env.CHANGE_BRANCH == 'feature1'
                }
            }
            steps {
                // Your deployment steps go here
                // For example:
                echo'kubectl apply -f deployment.yaml'
            }
        }
    }

    post {
        success {
            // Notify success
            echo 'Pipeline completed successfully!'
        }
        failure {
            // Notify failure
            echo 'Pipeline failed!'
        }
        always {
            // Execute build and test steps again for subsequent PRs
            if (env.CHANGE_TARGET == 'main' && env.CHANGE_BRANCH == 'feature1') {
                build job: 'jenkins_multi_branch', parameters: [string(name: 'BRANCH', value: 'feature1')]
            }
        }
    }
}
