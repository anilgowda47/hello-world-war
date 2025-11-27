pipeline {
    agent { label 'java' }

    stages {
        stage('update and install mvn') {
            steps {
                sh "sudo apt update -y"
              sh  "sudo apt install maven -y"
            }
        }
      
        stage('checkout') {
            steps {
                sh "rm -rf hello-world-war"
              sh  "git clone https://github.com/anilgowda47/hello-world-war.git"
            }
        }
         stage('Build - deploy') {
            steps {
                sh "mvn clean package"
            sh "sudo cp /home/slave1/workspace/war_pipeline/target/hello-world-war-1.0.1.war /opt/apache-tomcat-10.1.49/webapps"
            }
        }
    
      
    }
}
