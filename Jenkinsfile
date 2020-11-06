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
    stage ('Test docker image'){
      steps {
        sh 'docker run -d --rm --name testImages -p 8081:80 hisbu/project-pipeline'
        input message: "selesai test docker image? (Click procced to continue!)"
      }
    }
  }
}