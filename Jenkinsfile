pipeline {
    agent any
    environment {
        KUBECONFIG = 'C:\\Users\\hp\\.kube\\config'
    }
//The first stage is checking whether the namespace "wp" exists
    stages {
        stage('Check or Create Namespace') {
            steps {
                script {
                    def namespace = 'wp'
                    def namespaceExists = bat(returnStatus: true, script: "kubectl get namespace ${namespace}")
                    
                    if (!namespaceExists) {
                        echo "Namespace '${namespace}' exists."
                    } else {
                        echo "Namespace '${namespace}' does not exist. Creating..."
                        bat "kubectl create namespace ${namespace}"
                    }
                }
            }
        }
        // The second stage checks whether we have WordPress chart installed, if not, it will install it
        stage('Check and Install WordPress') {
            steps {
                script {
                    def chartName = 'wordpress'
                    def releaseName = 'final-project-wp-scalefocus'
                    def chartInstalled = bat(
                        script: "helm list -q ${releaseName}",
                        returnStatus: true
                    )
                    
                    if (chartInstalled != 0) {
                        dir('C:\\Users\\hp\\Desktop\\Final Project 777\\charts\\bitnami\\wordpress') {
                            bat 'helm dependency build .'  //using the bat command to escape the backslash on my Windows machine which was causing issues in my Pipeline build
                            bat "helm install ${releaseName} . -n wp -f values.yaml"
                        }
                    } else {
                        echo "WordPress chart is already installed."   // printing in the Jenkins console that WordPress is already installed if the previous steps are not true
                    }
                }
            }
        }
    }
}
