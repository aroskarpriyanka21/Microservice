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
                    serverUrl: 'https://DD3FC83615841AB8F0216B22A5CCB989.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh 'kubectl apply -f kubernetes-manifests/'
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
                    serverUrl: 'https://DD3FC83615841AB8F0216B22A5CCB989.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh 'kubectl get pods -n webapps'
                    sh 'kubectl get svc -n webapps'
                }
            }
        }
    }
}
