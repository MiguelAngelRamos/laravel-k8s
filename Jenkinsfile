pipeline {
    agent any
    stages {
        stage('Clonar YAML repo') {
            steps {
                git branch: 'main', url: 'https://github.com/MiguelAngelRamos/laravel-k8s.git'
            }
        }
        stage('Deploy en Kubernetes') {
            steps {
                sh '''
                    kubectl apply -f laravel-namespace.yaml
                    kubectl apply -f laravel-configmap.yaml
                    kubectl apply -f laravel-secret.yaml
                    kubectl apply -f laravel-pv-pvc.yaml
                    kubectl apply -f laravel-deployment.yaml
                    kubectl apply -f laravel-service.yaml
                    kubectl rollout status deployment laravel-deployment -n laravel-app
                '''
            }
        }
    }
}
