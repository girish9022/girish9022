pipeline {
    agent any

environment {
//         PATH = "/usr/bin:$PATH"
//         mvnHome= tool name: 'Maven_Paysquare', type: 'maven'
//         jdk = tool name: 'java', type: 'jdk'
//         JAVA_HOME = "${jdk}"
        
        DOCKER_REGISTRY="634842168668.dkr.ecr.ap-south-1.amazonaws.com"
        DOCKER_REPOSITORY="fmh"
        AWS_REGION="ap-south-1"
        IMAGE_TAG="check"
        
        //K8S variables
//         K8S_DEPLOYMENT_NAME="deliziahr-workflow"
//         K8S_DEPLOYMENT_CONTAINER_NAME="deliziahr-workflow"
//         K8S_NAMESPACE_NAME="test"

//         EKS_CLUSTER_NAME="qa-eks-cluster"


}
    stages {
//============================================================================================
	
        stage('Git Pull') {
            steps {
       git branch: 'new_test', credentialsId: 'girish_git', url: 'https://github.com/girish9022/girish9022.git'}
        }
//============================================================================================
       stage('Create Docker') {
            steps {
               sh "docker build -t $DOCKER_REGISTRY/$DOCKER_REPOSITORY:$IMAGE_TAG . -f dockerfile"
            }
        }
//============================================================================================        
        stage('ECR login'){
            steps {
               sh "aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $DOCKER_REGISTRY"
               sh "docker push $DOCKER_REGISTRY/$DOCKER_REPOSITORY:$IMAGE_TAG"
            }
        }
//============================================================================================        
//         stage('EKS cluster'){
//             steps{
//             // get kubeconfig
//             sh 'aws eks update-kubeconfig --region $AWS_REGION --name $EKS_CLUSTER_NAME' 
//             sh 'export KUBECONFIG=/var/lib/jenkins/.kube/config'
            
//             sh "kubectl delete deployment $K8S_DEPLOYMENT_NAME -n $K8S_NAMESPACE_NAME --kubeconfig /var/lib/jenkins/.kube/config"
//             sh 'sed -i "s,IMAGE_NAME,$DOCKER_REGISTRY/$DOCKER_REPOSITORY:$IMAGE_TAG," deployment.yaml'
//             sh "kubectl apply -f deployment.yaml -n $K8S_NAMESPACE_NAME --kubeconfig /var/lib/jenkins/.kube/config"
//             sh "docker rmi -f $DOCKER_REGISTRY/$DOCKER_REPOSITORY:$IMAGE_TAG"
//         }}
//============================================================================================        



    }}      
