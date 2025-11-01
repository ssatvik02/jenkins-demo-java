pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK25'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/<your-username>/jenkins-demo-java.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn -B clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn -B test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn -B package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**\\target\\*.war', fingerprint: true
                }
            }
        }

        stage('Deploy') {
            steps {
                bat """
                    echo Deploying WAR to Tomcat...
                    copy /Y target\\*.war "C:\\apache-tomcat-9.x\\webapps\\"
                """
            }
        }
    }
}
