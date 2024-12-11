pipeline {
    agent any
tools {
  maven 'maven3.9'
}
options {
  timestamps()
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '2', daysToKeepStr: '', numToKeepStr: '2')
}
triggers {
  //cron '* * * * *'
  githubPush()
  //pollSCM '* * * * *'
}
    stages {
        stage('checkoutcode') {
            steps {
                git 'https://github.com/pmmanoj650/maven-web-application.git'
            }
        }
        stage('Build') {
            steps {
                script {
                if (isUnix()){
                    sh 'mvn clean package'
                }
                else {
                bat 'mvn clean package'
            }
                }
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['ssh-agent-jenkins-pipelines']) {
    // some block
    sh 'scp -o StrictHostKeyChecking=no target/maven-web-application.war tomcat2@172.31.7.181:/opt/tomcat/webapps/'
            }
        }
    }
}
post {
  always {
    // One or more steps need to be included within each condition's block.
    sh 'echo "always condition"'
  }
  success {
    // One or more steps need to be included within each condition's block.
    sh 'echo "success condition"'
  }
  failure {
    // One or more steps need to be included within each condition's block.
    sh 'echo "failure condition"'
  }
}

}
