pipeline {
  agent any
  environment {
    CI = 'true'
    DOCKER_TAG = getDockerTag()
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
    stage ('Clean updocker test'){
      steps {
        sh 'docker stop testImages'
      }
    }
    stage ('push imate to registry'){
      steps {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub'){
          app.push("${DOCKER_TAG}")
          app.push("latest")
        }
      }
    }
  }
}

def getDockerTag(){
  def tag = sh script: "git rev-parse HEAD", returnStdout: true
  return tag
}