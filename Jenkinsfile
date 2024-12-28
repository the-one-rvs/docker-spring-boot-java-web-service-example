pipeline {
    agent any
    tools{
        jdk 'OpenJDK8'
        maven 'jenkins-maven'
        
    }

    stages {
        stage('SCM') {
            steps {
                git changelog: false, poll: false, url: 'https://github.com/the-one-rvs/docker-spring-boot-java-web-service-example'
            }
        }
        stage('Build Maven') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Docker build and run') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-hub-credentials') {
                        // some block
                        sh "docker build -t quasarcelestio/example:latest . "
                        sh "docker push  quasarcelestio/example:latest"
                    }
                }
            }
        }
    }
}
