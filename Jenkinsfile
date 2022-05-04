pipeline {
    agent any
    tools { 
        maven 'LocalMaven' 
        jdk 'LocalJDK' 
    }
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f /var/lib/jenkins/workspace/build-tomcat-docker-image/pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "ls -a"
                sh "docker build -t tomcatsamplewebapp:${env.BUILD_ID} /var/lib/jenkins/workspace/build-tomcat-docker-image/Dockerfile"
            }
        }

    }
    
}