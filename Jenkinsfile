pipeline {
  agent any

  stages {
    stage('Check and Create Namespace') {
      steps {
        script {
          def namespace = 'wp'

          // Check if the namespace exists
          def namespaceExists = sh(returnStdout: true, script: "kubectl get namespace ${namespace} -o name || echo ''").trim()

          if (namespaceExists == '') {
            // Namespace doesn't exist, create it
            sh "kubectl create namespace ${namespace}"
            echo "Namespace ${namespace} created"
          } else {
            echo "Namespace ${namespace} already exists"
          }
        }
      }
    }

    stage('Check and Install WordPress') {
      steps {
        script {
          def releaseName = 'wordpress'
          def chartVersion = 'stable/wordpress'

          // Check if WordPress release is already installed
          def releaseStatus = sh(returnStatus: true, script: "helm status ${releaseName} > /dev/null 2>&1 || echo 'not-found'").trim()

          if (releaseStatus == 'not-found') {
            // WordPress release not found, install the chart
            sh "helm install ${releaseName} ${chartVersion} --namespace wp"
            echo "WordPress chart installed"
          } else {
            echo "WordPress chart already installed"
          }
        }
      }
    }
  }
}
