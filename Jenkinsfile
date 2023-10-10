node {
    withDockerContainer(args: '-v /root/.m2:/root/.m2', image: 'maven:3.9.4-eclipse-temurin-17-alpine') {
        stage('Build') {
            sh 'echo "Hello World"'
        }
    }
}