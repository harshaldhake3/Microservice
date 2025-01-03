pipeline {
    agent any

    stages {
        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig(
                    credentialsId: 'kubernetes-cp', 
                    serverUrl: 'https://192.168.1.22:6443', 
                    namespace: 'webapps', 
                    contextName: '', // Specify the context name if available
                    clusterName: 'kubernetes', 
                    restrictKubeConfigAccess: false
                ) {
                    sh 'kubectl apply -f deployment-service.yml --validate=false'
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withKubeConfig(
                    credentialsId: 'kubernetes-cp', 
                    serverUrl: 'https://192.168.1.22:6443', 
                    namespace: 'webapps', 
                    contextName: '', // Specify the context name if available
                    clusterName: 'kubernetes', 
                    restrictKubeConfigAccess: false
                ) {
                    sh 'kubectl get svc -n webapps'
                }
            }
        }
    }
}
