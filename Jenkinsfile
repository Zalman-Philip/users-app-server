pipeline {
    agent any

    stages {
        stage('Build users server') {
            steps {
                script {
                echo 'Building...'
                // Add your build steps here
                }
            }
        }

        stage('Lint users server') {
            steps {
                script {
                echo 'Linting...'
                sh 'npm i'
                sh 'npm run lint'
                // Add your linting steps here
                }
            }
        }
    }
    post {
        success {
            script {
                echo 'Linting passeeed. You may now merge.'
            }
        }
        failure {
            script {
                echo 'Pipeline failed. Blocking pull request merge.'
            }
        }
    }
}
