pipeline {
  agent any
  stages {
    stage('git update') {
      steps {
        git url: 'https://github.com/LeeJinyeong218/kakaodevpipeline.git', branch: 'main'
      }
    }

    stage('docker update and push') {
      steps {
        sh '''
        sudo docker build -t leejinyeong/kakaodev:yellow .
        sudo docker push leejinyeong/kakaodev:yellow
        '''
      }
    }

    stage('kubernetes deploy service') {
      steps {
      sh '''
      ssh 211.183.3.100 'kubectl create deploy-yellow --image=leejinyeong/kakaodev:yellow'
      ssh 211.183.3.100 'kubectl expose deploy deploy-yellow --type=NodePort --port=8004 --target-port=80 --nodePort=30004 --name=deploy-yellow-np'
      '''
      }
    }
  }
}