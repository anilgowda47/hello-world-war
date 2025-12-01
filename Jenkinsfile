pipeline {
    // agent { label 'java' }
    agent none
    parameters {
        string(name: 'mcmd1', defaultValue: 'clean', description: 'maven clean command')
        booleanParam(name: 'SAMPLE_BOOLEAN', defaultValue: true, description: 'A boolean parameter')
        choice(name: 'mcmd2', choices: ['package', 'compile', 'install', 'validate'], description: 'Choose one option')
    }
    stages {
        stage ('hello-world-war') {
            parallel {
                stage('Checkout') {
                    agent { label 'java' }
                    steps {
                        withCredentials([
                            usernamePassword(credentialsId: '7b5f13d2-07bd-4361-b9eb-61a78db4146d',
                                usernameVariable: 'MY_USERNAME',
                                passwordVariable: 'MY_PASSWORD'),
                            sshUserPrivateKey(credentialsId: '5b90b9a6-bae4-44c9-b4e6-6498c4b154ff',
                                keyFileVariable: 'KEY_FILE',
                                usernameVariable: 'SSH_USER')
                        ]) {
                            sh "rm -rf hello-world-war"
                            sh "git clone https://github.com/anilgowda47/hello-world-war"
                        }
                    }
                }

                stage('Build') {
                    agent { label 'java' }
                    steps {
                        sh "mvn $mcmd1 $mcmd2"
                    }
                }
            }
        }

        stage('Deploy') {
            agent { label 'java' }
            steps {
                sh "sudo cp /home/slave1/workspace/war_pipeline/target/hello-world-war-1.0.1.war /opt/apache-tomcat-10.1.49-src/webapps"
            }
        }
    }
}
