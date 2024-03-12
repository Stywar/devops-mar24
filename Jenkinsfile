pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                git branch: 'master' , url: 'https://github.com/Stywar/devops-mar24'
            }
        }
        
        stage('Builder Image') {
            steps {
              bat(script: 'docker build -t antony0618/devops-mar24 .' ,returnStdout:true); 
              bat(script: 'docker push antony0618/devops-mar24' ,returnStdout:true); 
            }
        }
        
        stage ('CD AKS') {
            steps {
                
             bat(script: 'az login --service-principal --username 60445a5a-4c7d-404e-96a0-0d5c83c4978f --password T7V8Q~Zo-Ie9YyVyFw.FeCbw3wma~ZP~ghI.1b.~ --tenant 74343d69-5375-4c7a-8cc9-08986488c964' ,returnStdout:true);
             bat(script: 'az account set --subscription a29dad22-fa1e-4b41-ace0-4159a70e3816' ,returnStdout:true);
             bat(script: 'az aks get-credentials --resource-group Devops --name devopsmar24 --overwrite-existing' ,returnStdout:true);
             bat(script: 'kubectl config get-contexts --kubeconfig=%KUBE_PATH_CONFIG%' ,returnStdout:true);
             bat(script: 'kubectl config use-context devopsmar24 --kubeconfig=%KUBE_PATH_CONFIG%' ,returnStdout:true);
             bat(script: 'kubectl apply -f k8s.yml --kubeconfig=%KUBE_PATH_CONFIG%' ,returnStdout:true);
             
            }
        }
    }
}
