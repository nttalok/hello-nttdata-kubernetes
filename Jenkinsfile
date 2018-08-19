//Jenkinsfile
node {
	stage('setup k8s') {
		println("k8s setup done")
	}
	stage('Clone repository') {

        // clone git repo
		git url:'https://github.com/nttalok/hello-nttdata-kubernetes.git'
    }
	stage('integrationTest') {
	 
		withKubeConfig([credentialsId: 'k8s-caas-demo-config',serverUrl: 'https://10.91.177.119:6443']) {
		  
			 sh 'kubectl apply -f ./ --namespace=caas-demo-test'
			 println("pod deployed")
			 println("Integration done, Cleaning deployment")
			 sh 'kubectl delete -f hello-ntt-data.yaml --namespace=caas-demo-test'
			 println("integrationTest complete")
		}
	}

	stage('prod') {
	 
		withKubeConfig([serverUrl: 'https://10.91.177.119:6443']) {
		  
			 sh 'kubectl apply -f hello-ntt-data.yaml --namespace=caas-demo-prod'
			 println("pod deployed")
		}
	}	

	stage('prodValidate') {
		println("prod validation completed")

	}	
   
}