pipeline {
  agent {
    label 'vm'
  }
  stages {
    stage('deploy symfony PROD/HA') {
      when {
        branch 'main'
      }
      steps {
        sh """
          helm upgrade -f ./demo/values-ha.yaml symfony ./demo --install --namespace symfony-prod --create-namespace --wait
        """
      }
    }
    stage('deploy symfony non PROD') {
      when {
        not {
          branch 'main'
        }
      }
      steps {
        sh """
         helm upgrade symfony ./demo --install --namespace symfony-dev --create-namespace --wait
        """
      }
    }
  }
  post {
    failure {
      sh "helm rollback symfony"
    }
    always {
      cleanWs()
    }
  }
}
