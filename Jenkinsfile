pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the repository
                git branch: '*/main', url: 'https://github.com/your/repository.git'
            }
        }
        stage('Build') {
            steps {
                // Your build steps go here
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                // Your test steps go here
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            when {
                // Trigger the stage only if the branch is 'main' and the event is a pull request
                expression { env.CHANGE_BRANCH == 'main' && env.CHANGE_ID != null }
            }
            steps {
                // Your deployment steps go here
                sh 'deploy.sh'
            }
        }
    }
    
    // Post actions
    post {
        success {
            // Your success actions go here
            echo 'Pipeline succeeded!'
        }
        failure {
            // Your failure actions go here
            echo 'Pipeline failed!'
        }
    }
}
