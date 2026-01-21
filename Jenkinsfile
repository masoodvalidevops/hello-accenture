pipeline {
    agent any

    tools {
        maven 'Maven-3.9.9'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/<your-username>/hello-accenture.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=hello-accenture \
                    -Dsonar.projectName=hello-accenture
                    '''
                }
            }
        }

        stage('Upload Artifact to Nexus') {
            steps {
                sh 'mvn deploy -DskipTests'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                sudo rm -rf /opt/tomcat/webapps/hello-accenture*
                sudo cp target/hello-accenture.war /opt/tomcat/webapps/
                '''
            }
        }
    }
}

