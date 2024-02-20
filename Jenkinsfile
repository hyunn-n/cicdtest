pipeline {
  agent any
  stages {
    stage('git clone update') {
      steps {
        git url: 'https://github.com/hyunn-n/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        docker build -t hynnx/cicdtest:green .
        docker push hynnx/cicdtest:green
        '''
      }
    }
    stage('deploy kubernetes') {
      steps{
        sh '''
        kubectl create deployment grweb --image=hynnx/cicdtest:green
        kubectl expose deployment grweb --type=LoadBalancer --port=80 \
                                           --target-port=80 --name=grweb
        '''
     }
    }
  }
}
