node {
    try {
        // Stage Build
        stage('Build') {
            def mavenImage = docker.image('maven:3.9.4-eclipse-temurin-17-alpine').inside("-v /root/.m2:/root/.m2") {
                sh 'mvn -B -DskipTests clean package'
            }
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}
