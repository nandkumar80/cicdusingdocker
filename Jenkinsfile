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
	}
}
