pipeline {
    agent { docker 'maven:3.9.3-eclipse-temurin-17' }


    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/Sanjitoncuistot/Projet'

                // Run Maven on a Unix agent.
                sh "mvn -f rest-service/pom.xml -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/rest-service/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'rest-service/target/*.jar'
                }
            }
        }
    }
}
