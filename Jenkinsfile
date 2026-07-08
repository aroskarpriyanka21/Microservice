pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '',
                    clusterName: 'EKS-1',
                    contextName: '',
                    credentialsId: 'k8-secret',
                    namespace: 'webapps',
                    serverUrl: 'https://5B2106746622D1549584DD686850D4FB.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh 'kubectl apply -k kubernetes-manifests/'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '',
                    clusterName: 'EKS-1',
                    contextName: '',
                    credentialsId: 'k8-secret',
                    namespace: 'webapps',
                    serverUrl: 'https://5B2106746622D1549584DD686850D4FB.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh 'kubectl get pods -n webapps'
                    sh 'kubectl get svc -n webapps'
                }
            }
        }
    }
}
