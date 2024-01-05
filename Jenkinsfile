pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    
    environment {
        SONARQUBE_HOME = tool 'SonarQubeScanner'
        // Puedes agregar otras variables de entorno necesarias aquí
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Puedes realizar acciones de construcción aquí
                    echo 'Hello World'
                    sh "mvn -Dmaven.test.failure.ignore=true clean package"
                }
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
                    withSonarQubeEnv('SonarQube') {
                        def sonarProjectKey = 'com.calidadDelSofware:practica4'
                        sh "${SONARQUBE_HOME}/bin/sonar-scanner -Dsonar.java.binaries=target/classes -Dsonar.projectKey=${sonarProjectKey} -X"
                    }
                }
            }
        }
    }
    post {
        always {
            // Puedes agregar acciones posteriores aquí, como la publicación de informes o notificaciones
            junit(allowEmptyResults: true, testResults: '*test-reports/*.xml')
        }
    }
}


