node {
    try {
        stage('Build') {
            def mavenImage = docker.image('maven:3.9.4-eclipse-temurin-17-alpine').inside("-v /root/.m2:/root/.m2") {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        
        stage('Test') {
            try {
                def mavenImage = docker.image('maven:3.9.4-eclipse-temurin-17-alpine').inside("-v /root/.m2:/root/.m2") {
                    sh 'mvn test'
                } 
            }    
            finally {
                junit 'target/surefire-reports/*.xml'
            }
        }
        stage('Deploy') {
            def mavenImage = docker.image('maven:3.9.4-eclipse-temurin-17-alpine').inside("-v /root/.m2:/root/.m2") {
                    sh './jenkins/scripts/deliver.sh'
                    sleep 60
                    sh './jenkins/scripts/kill.sh'
            } 
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}