pipeline {
    agent any

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
            
            }
        }
    
      
    }
}
