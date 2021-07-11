pipeline {
  agent any
  stages {
    stage('clone') {
      steps {
        git(url: 'https://github.com/ssp339cloud/spring-bop.git', branch: 'master')
      }
    }

    stage('maven ') {
      steps {
        sh 'mvn package'
      }
    }

    stage('deploy to tomcat') {
      steps {
        sh 'curl -v -u tomcatcred -T //var/lib/jenkins/workspace/spring-bop1_master/target/spring3-mvc-maven-xml-hello-world-1.0-SNAPSHOT.war \'http://ec2-100-26-149-72.compute-1.amazonaws.com:8181/manage/text/deploy?path=spring_pipeline&update=true\''
      }
    }

  }
}