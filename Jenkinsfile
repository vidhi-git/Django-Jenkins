pipeline{
 agent any
 
 stages{
	stage("Clone Code"){
	 steps{
	 echo "Cloning the codde"
	 git url:"https://github.com/vidhi-git/Django-Jenkins.git", branch: "main"
	 } 
	}
	 stage("build"){
	 steps{
	 echo "Building the image"
	 sh "docker build -t my-note-app ."
	 }
	 }
	 stage("Push to Docker Hub"){
	 steps{
	 echo "Pushing the image to docker hub"
	 withCredentials([usernamePassword(credentialsId:"Jenkins",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")])
		{
		sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
		 sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
		 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
		 sh "docker push ${env.dockerHubUser}/my-note-app:latest"


		}
	 }
	 }
 
	 stage("Deploy"){
	 steps{
	 echo "Deploying"
	 sh "docker-compose down && docker-compose up -d"
	 }
	 }
	}
	}

