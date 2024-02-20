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
        sudo docker build -t hynnx/cicdtest:green .
        sudo docker push hynnx/cicdtest:green
        '''
      }
    }
    stage('deploy kubernetes') {
      steps{
        sh '''
        ansible master -m command -a 'kubectl create deployment grweb --image=hynnx/cicdtest:green'
        ansible master -m command -a 'kubectl expose deployment grweb --type=LoadBalancer --port=80 \
                                           --target-port=80 --name=grweb'
        '''
     }
    }
  }
}
