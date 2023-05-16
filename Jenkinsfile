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

    stage('Deploy Helm Chart') {
      steps {
        script {
          def releaseName = 'wordpress'
          def chartVersion = 'stable/wordpress'
          def chartValuesFile = '/Users/hp/Desktop/Final Project 7/charts/bitnami/wordpress/values.yaml'

          // Install or upgrade the Helm chart
          sh "start /B helm upgrade --install ${releaseName} ${chartVersion} --namespace wp -f ${chartValuesFile}"
          echo "Helm chart deployed or upgraded"
        }
      }
    }
  }
}
