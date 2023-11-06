pipeline {
  agent {
    label 'vm'
  }
  stages {
    stage('deploy symfony HA') {
      when {
        branch 'main'
      }
      steps {
        sh "helm upgrade -f ./demo/values-ha.yaml symfony ./demo'
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
         helm upgrade symfony ./demo
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
