pipeline {
  agent any
  environment {
    CI = 'true'
  }

  stages {
    stage ('Install Dependencies react project') {
      steps {
        echo 'Start install dependencies react project'
        sh 'npm install'
      }
    }
    stage('Test project'){
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Build Project react'){
      steps{
        sh 'npm run build'
      }
    }
    stage ('Build DOcker Image'){
      steps {
        script {
          app = docker.build("hisbu/project-pipeline")
        }
      }
    }
  }
}