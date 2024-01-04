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
        stage('SCM') {
            steps {
                checkout scm
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    def mvn = tool 'Maven';
                    withSonarQubeEnv() {
                        echo 'Starting SonarQube Analysis...'
                        sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=SonarQubeJenkins-Practica4 -Dsonar.projectName='SonarQubeJenkins-Practica4'"
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

