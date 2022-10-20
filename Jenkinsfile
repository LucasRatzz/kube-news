pipeline {
     agent any 

     stages { 
        stage ('Build Docker Image') {
            steps {
                script {
                    // var que representa a Docker Image
                    dockerapp = docker.build("lucasratzz/kube-news:${env.BUILD_ID}", "-f ./src/Dockerfile ./src")
                }
            }
        }

        stage ('Push Docker Image') {
            steps {
                script {
                   docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")


                }
            }
        }
        // CI /\
        // CD \/
        stage ('Deploy Kubernetes') {
            steps {
                withKubeconfig ([credentialsID: 'kubeconfig']) {
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }
        }
        
     }
}