node {
    stage('Build') {
        docker.image('maven:3.9.0-eclipse-temurin-11').inside('-v /root/.m2:/root/.m2') {
            sh 'mvn -B -DskipTests clean package'
        }
    }
    stage('Test') {
        docker.image('maven:3.9.0-eclipse-temurin-11').inside('-v /root/.m2:/root/.m2') {
            sh 'mvn test'
        }
        //post {
          //  always {
          //      junit 'target/surefire-reports/*.xml'
          //  }
        //}
    }
    stage('Deliver') {
        // Modify the path to deliver.sh according to your project structure
        sh './jenkins/scripts/deliver.sh'
    }
}
