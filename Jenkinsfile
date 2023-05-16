pipeline {
   agent any

   environment {
      KUBECONFIG = '/var/lib/jenkins/.kube/config'
   }

   stages {
      stage('Checking if the namespace exists') {
            steps {
               script {
                  def wpNamespace = sh(script: 'kubectl get namespace wp', returnStatus: true) == 0
                  if (!wpNamespace) {
                      echo 'Creating the wp namespace'
                       sh 'kubectl create namespace wp'
                        
                        return
                  } else {
                       echo 'Namespace wp exists'
                  }
               }
            }
      }

      stage('Installing WordPress through Helm') {
            steps {
               script {
                  sh 'helm dependency build ./bitnami/wordpress'
                  sh 'helm upgrade --install final-project-wp-scalefocus ./bitnami/wordpress -n wp'
               }
            }
      }
   }
}
