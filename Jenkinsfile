pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Hello World'
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                        sh "${mvnHome}/bin/mvn sonar:sonar"
                    }
                }
            }
        }
    }
    post {
        always {
            junit(
                allowEmptyResults: true,
                testResults: '*test-reports/*.xml'
            )
        }
    }
}
