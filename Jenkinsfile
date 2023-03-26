pipeline {
	agent any 
	tools{
	maven "M2_HOME"
	}
	stages{
	stage('git checkout'){
	steps{
	 checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '25b2c6b9-167b-4411-8eab-ba222b3dcb8d', url: 'https://github.com/nandkumar80/cicdusingdocker.git']])

	}
	}
	stage('build using maven'){ 
		steps{	

	sh 'mvn clean package'
		}
		}

	stage('build docker image and tag'){
	  steps{
	sh 'who && pwd'	  
	 sh 'docker build -t samplewebapp:latest .'
	 sh 'docker tag samplewebapp nandkumar80/samplewebapp:$BUILD_NUMBER'
	 }
	}
	stage('docker image push to dockerhub'){
	 steps{
	   withCredentials([string(credentialsId: 'dockerhubpasswd', variable: 'dockerhubpwd')]) {
       sh 'docker push nandkumar80/samplewebapp:$BUILD_NUMBER' 
	}
	 }
	}
	stage('Run Docker container on Jenkins Agent'){
	steps{
	sh "docker run -d --name webcontainer -p 8003:8080 nandkumar80/samplewebapp$BUILD_NUMBER"
	}
	}
	}
}
