pipeline {
    agent any

    stages {   
        stage('Build with maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install'
            }
        }
        
        stage('Test') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        
            }
        stage('Code Qualty Scan Analysis') {
           steps {
                  withSonarQubeEnv('sonar_server') {
             sh "mvn -f SampleWebApp/pom.xml sonar:sonar"      
               }
            }
       }

        stage('Quality Gate Scanner') {
            steps {
               waitForQualityGate abortPipeline: true
            }
      }


        stage('push to nexus Artifactory') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'SampleWebApp', classifier: '', file: 'SampleWebApp/target/SampleWebApp.war', type: 'war']], credentialsId: 'nexus_ID', groupId: 'SampleWebApp', nexusUrl: '3.142.69.69:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snaphots', version: '1.0-SNAPSHOT'
            }   
            
        }
        
        stage('deploy to tomcat') {
          steps {
            deploy adapters: [tomcat9(credentialsId: 'tomcat_ID', path: '', url: 'http://18.220.176.165:8080')], contextPath: 'webapp', war: '**/*.war'
             
            }
            
        }
            
    }
} 
