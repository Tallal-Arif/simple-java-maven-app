pipeline {
    agent any

    tools {
        maven 'Maven'        // Must match the name in Jenkins Global Tool Config
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo 'Deploying to Tomcat...'
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-credentials',
                        path: '',
                        url: 'http://localhost:8080'
                    )
                ],
                contextPath: 'myApp',
                war: 'target/*.jar'
            }
        }

    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
