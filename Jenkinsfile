pipeline {
    agent {
        docker {
            image 'maven:3.9.2-jdk-11-slim' // Or your custom image
            args '-u 1000:1000' //Run as user 1000:1000 (Common Jenkins user)
            volumes {
                hostPath "${env.WORKSPACE}/.m2"
                containerPath "/root/.m2"
            }
        }
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/mbahnizen/simple-java-maven-app.git', branch: 'first-submission'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
