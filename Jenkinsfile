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
              deploy adapters: [tomcat9(credentialsId: 'tomcat_ID', path: '', url: 'http://3.16.26.232:8080')], contextPath: 'Webapp', war: '**/*.war'
            }
        }
    }
}
