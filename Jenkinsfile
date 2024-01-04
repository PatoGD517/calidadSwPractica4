pipeline {
    agent any
    tools{
        maven 'Maven'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Hello World'
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
    }
    post{
        always{
            junit(
                allowEmptyResults:true,
                testResults: '*test-reports/.xml')
        }
    }
}
