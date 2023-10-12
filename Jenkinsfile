node {
    try {
        stage('Build') {
            def mavenImage = docker.image('maven:3.9.4-eclipse-temurin-17-alpine').inside("-v /root/.m2:/root/.m2") {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        
        stage('Test') {
            def mavenImage = docker.image('maven:3.9.4-eclipse-temurin-17-alpine').inside("-v /root/.m2:/root/.m2") {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}