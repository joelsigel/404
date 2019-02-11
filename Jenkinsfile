pipeline {
    agent any

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }

    stages {
        stage('Build') {
            steps {
                sh 'echo "Building..."'
                slackSend channel: '#jenkins',
                  color: 'good',
                  message: "The pipeline ${currentBuild.fullDisplayName} is building..."
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Testing..."'
            }
        }
    }

    post {
        always {

        }
        success {
          slackSend channel: '#jenkins',
            color: 'good',
            message: "The pipeline ${currentBuild.fullDisplayName} was built successfully."
        }
        failure {
          slackSend channel: '#jenkins',
            color: 'danger',
            message: "The pipeline ${currentBuild.fullDisplayName} has failed."
        }
        unstable {
          slackSend channel: '#jenkins',
            color: 'danger',
            message: "The pipeline ${currentBuild.fullDisplayName} is unstable."
        }
        changed {
          slackSend channel: '#jenkins',
            color: 'warning',
            message: "The pipeline ${currentBuild.fullDisplayName} has branch changes."
        }
    }

}
