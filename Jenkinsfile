node {
    stage('Build') {
        withDockerContainer(image: 'maven:4.0.0', args: '-v /root/.m2:/root/.m2') {
            sh 'mvn -B -DskipTests clean package'
        }
    }
    stage('Test') {
        withDockerContainer(image: 'maven:4.0.0', args: '-v /root/.m2:/root/.m2') {
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
