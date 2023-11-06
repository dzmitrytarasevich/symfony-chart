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
        sh "helm install -f ./demo/values-ha.yaml symfony ./demo --namespace symfony-prod --create-namespace --wait'
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
         helm install symfony ./demo --namespace symfony-dev --create-namespace --wait
        """
      }
    }
  }
  post {
    failure {
      sh "helm rollout symfony"
    }
    always {
      cleanWs()
    }
  }
}
