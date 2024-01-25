pipeline {
    agent any 
    
    tools {
        maven 'apache_maven'
    }
    
    stages {
        stage('Clonerepo') {
            steps {
                git 'https://github.com/bhasker-manikyala/DevOpsClassCodes.git'
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('CodeReview') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('UnitTesting'){
            steps {
                sh 'mvn test'
            }
        }
        stage('Codecoverage'){
            steps {
               sh 'mvn verify'   
            }
        }
        stage('Package'){
            steps {
               sh 'mvn package'
                post {
                  success {
                        sshagent(['f8407f6e-29bd-422e-a339-1ce0ce705eef']) {
		                    sh 'scp /var/lib/jenkins/workspace/addressBoo Pipeline Project/target/addressBook.war ubuntu@54.227.203.231:/home/ubuntu/tomcat/webapps '
	                            }
                          }
                    }
            }
        }
    }
}
