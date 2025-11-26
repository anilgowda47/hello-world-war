pipeline {
            agent any
stage('update and install') {
            steps {
sh "sudo apt update"
sh "sudo apt install maven -y"
            }
        }
            stages {
                stage('checkout') {
            steps {
                sh "git clone https://github.com/anilgowda47/hello-world-war/new/master"
            }
        }
    }
}
