pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage ('Deploy Backend') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'TomcatLogin', path: '', url: 'http://localhost:8002/')], contextPath: 'asks-backend', war: 'target/tasks-backend.war'
            }
        }

        stage ('API Test') {
            steps {
                git credentialsId: 'github_login', url: 'https://github.com/luhcapellini/tasks-api-test'
                sh 'mvn test'
            }
        }
    }
}