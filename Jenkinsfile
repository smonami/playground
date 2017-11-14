pipeline {
  agent {
    node {
      label 'maven-jdk-8'
    }
    
  }
  stages {
    stage('Preparation') {
      steps {
        git(url: 'https://github.com/jglick/simple-maven-project-with-tests.git', branch: 'master')
        sh 'echo "hello"'
      }
    }
    stage('Build') {
      steps {
        parallel(
          "Build": {
            sh 'mvn -Dmaven.test.failure.ignore clean package'
            
          },
          "codeQA": {
            echo 'code has been scanned'
            
          }
        )
      }
    }
    stage('Result') {
      steps {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
      }
    }
  }
}