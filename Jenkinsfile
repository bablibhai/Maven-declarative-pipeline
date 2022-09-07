pipeline {
    agent { label 'Devops-node' }
    tools {
    maven 'maven3.8.6'
    }
    triggers {
        pollSCM 'H * * * *'
    }
    stages {
        stage('clone') {
            steps {
                git 'https://github.com/bablibhai/java-web-app-docker.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('archive artifacts') { 
            steps {
                archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false 
            }
            
        }
        stage('deploy') { 
            steps {
               deploy adapters: [tomcat9(credentialsId: 'admin1', path: '', url: 'http://13.234.119.218:8080/')], contextPath: null, war: '**/*.war'            }            
        }
          
    }
}
