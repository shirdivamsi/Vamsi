pipeline {
    agent any
    tools {
        maven 'maven-3.9.6'
    }
    stages {
        stage("Build") {
            steps {
                script {
                    sh "mvn clean package"
                }
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: "**/target/*.war"
                }
            }
        }

        stage('Deploy to Tomcat Server') {
            steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: 'tomcat-user', path: '', url: 'http://18.191.114.10:8081/')], contextPath: null, war: '**/*.war'
                }
            }
        }
    }
}
