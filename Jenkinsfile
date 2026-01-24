pipeline {
    agent any
   
    tools {
        maven 'Maven-3.9.9'
        jdk 'Java-17'
    }

    stages {
        stage('git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-creds', url: 'https://github.com/masoodvalidevops/hello-accenture.git'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube-server') {
                    sh 'mvn clean verify sonar:sonar'
                }
            }
        }

        stage('Upload Artifact to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'hello-accenture', classifier: '', file: 'target/hello-accenture.war', type: '.war']], credentialsId: 'Nexus_jenkins', groupId: 'com.accenture', nexusUrl: '43.205.210.57:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'msd-nexus', version: '1.0'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcat-Jenkins', path: '', url: 'http://13.126.115.148:9090')], contextPath: null, war: 'target/hello-accenture.war'
                
            }
        }
    }
}
