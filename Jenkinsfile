pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                sh 'cd SampleWebApp mvn test'
            }
        }
        stage('Build') {
            steps {
                sh 'cd SampleWebApp && mvn clean package'
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
              deploy adapters: [tomcat9(credentialsId: 'tomcatserver_ID', path: '', url: 'http://52.15.231.68:8080')], contextPath: 'webapp', war: '**/*.war'
            }
        }
    }
}
