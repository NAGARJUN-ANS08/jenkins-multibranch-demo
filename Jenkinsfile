pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Building branch: ${env.BRANCH_NAME}"
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -B clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn -B test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn -B package -DskipTests'
                archiveArtifacts artifacts: 'target/*.jar',
                    fingerprint: true
            }
        }
    }

    post {
        success {
            echo "CI pipeline succeeded for branch: ${env.BRANCH_NAME}"
        }

        failure {
            echo "CI pipeline failed for branch: ${env.BRANCH_NAME}"
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
