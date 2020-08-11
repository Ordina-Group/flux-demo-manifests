pipeline {
    agent any
    stages {
    stage('download helm') {
        steps {
            sh """
            curl -fsSL -o helm.tar.gz https://get.helm.sh/helm-v3.2.4-linux-amd64.tar.gz
            tar xf ./helm.tar.gz
            mv ./linux-amd64/helm ./helm
            chmod 700 ./helm
            """
        }
      }
      stage('template with helm') {
        steps {
            sh './helm template charts/game'
        }
      }
   }
}
