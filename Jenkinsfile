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

  }
}