pipeline {
    agent any
    parameters {
        choice(name: 'image', choices: 'edserbin/flappy_bird\nalexwhen/docker-2048:latest')
    }
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
            sh "./helm template charts/game --set image=${params.image} > ./test/deployment.yaml"
        }
      }
      stage('add to git') {
        steps {
          sshagent(credentials : ["basGithubSshKey"]) {
              sh """
              git status
              git add ./test/deployment.yaml 
              git commit -m '[${JOB_NAME}:${BUILD_NUMBER}] manifests updated.\n${BUILD_URL}'
              git push
              """
          }
        }
      }
   }
}
