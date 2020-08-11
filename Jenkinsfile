pipeline {
    agent any
    stages {
    stage('download helm') {
        steps {
            sh """
            curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
            chmod 700 get_helm.sh
            ./get_helm.sh
            """
        }
      }
      stage('template with helm') {
        steps {
            sh 'helm --version'
        }
      }
   }
}
