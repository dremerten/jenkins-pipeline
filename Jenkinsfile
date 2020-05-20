pipeline {

  agent { label 'k8_jpipeline_pod' }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://gitlab.com/andre.merten/jenkins-pipeline.git', branch:'master'
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "nginx.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
