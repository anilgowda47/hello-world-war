pipeline {
   // agent { label 'java' }
agent none
    stages {
        stage('hello world war') {
            parallel {
                stages('checkout') {
                    agent { label 'java' }
                    steps {
                        sh "rm -rf hello-world-war"
                        sh "git clone https://github.com/anilgowda47/hello-world-war.git"
                    }
                }
                stage('Build') {
                    agent { label 'java' }
                    steps {
                        sh "mvn clean package"
                    }
                }
                stage('Deploy') {
                    agent { label 'java' }
                    steps {
                sh "sudo cp /home/slave1/workspace/war_pipeline/target/hello-world-war-1.0.1.war /opt/apache-tomcat-10.1.49/webapps"
                    }
                }
            }
        }
    }
}
}

