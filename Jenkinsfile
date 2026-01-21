pipeline {
    agent any

    tools {
        maven 'Maven-3.9.9'
        jdk 'Java-17'
    }

    stages {
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo "SonarQube step will be added"
            }
        }

        stage('Upload Artifact to Nexus') {
            steps {
                echo "Nexus upload step will be added"
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo "Tomcat deploy step will be added"
            }
        }
    }
}

