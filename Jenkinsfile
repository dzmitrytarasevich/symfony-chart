pipeline {
  agent {
    label 'vm'
  }
  stages {
    stage('helm install image') {
      steps {
        sh """
         helm upgrade symfony ./demo
        """
      }
    }
  }
  post {
    failure {
      sh "helm upgrade symfony"
    }
    always {
      cleanWs()
    }
  }
}
