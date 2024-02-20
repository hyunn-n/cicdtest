pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: '', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        docker build -t hynnx/cicdtest:blue .
        docker push hynnx/cicdtest:blue
        '''
      }
    }
    stage('deploy kubernetes') {
      steps{
        sh '''
        kubectl create deployment cicdblue --image=hynnx/cicd:blue
        kubectl expose deployment cicdblue --type=LoadBalancer --port=80 \
                                              --target-port=80 --name=cicdblue
        '''
     }
    }
  }
}
