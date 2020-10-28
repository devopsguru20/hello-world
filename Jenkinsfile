pipeline {
    agent any
    environment {
        PATH = "/usr/share/maven/bin:$PATH"
    }
    stages {
        stage("clone code"){
            steps{
               git credentialsId: 'git_credentials', url: 'https://github.com/aws2020training/hello-world.git'
            }
        }
        stage("build code"){
            steps{
              sh "mvn clean install"
            }
        }
        stage("deploy"){
            steps{
              sshagent(['ubuntu']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ubuntu@172.31.7.55:/home/ubuntu/apache-tomcat-8.5.54/webapps"
                 
                }
            }
        }
    }
}
