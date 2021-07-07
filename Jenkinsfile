pipeline {
    agent any
    tools {
       maven "Maven3"
    }
    stages {
        stage ('get scm') {
            steps {
                git credentialsId: 'gitub_credentials', url: 'https://github.com/ssp339cloud/spring3-mvc-maven-xml-hello-world.git'
            }
        }
        stage ('mvn build') {
            steps {
              sh "mvn package"
            }
        }
        stage ('archive artifact') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
            }
        }
        stage ('deploy to tomacat') {
            steps {
                withCredentials([usernameColonPassword(credentialsId: 'tomcat_credentials', variable: 'tomcatcred')]) {
               sh "curl -v -u tomcatcred -T /var/lib/jenkins/workspace/spring_pipeline/target/spring3-mvc-maven-xml-hello-world-1.0-SNAPSHOT.war 'http://ec2-3-239-160-31.compute-1.amazonaws.com:8181/manage/text/deploy?path=spring_pipeline&update=true'"
        }
            }
    }
  }
  post {
        failure {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

        always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "ssp339.cloud@gmail.com",
                sendToIndividuals: true])
        }
  }
}
