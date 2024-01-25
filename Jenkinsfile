pipeline{
	
	agent any

	stages{
		stage("Code"){
			steps{
				git url: "https://github.com/aakashgoel2002/node-todo-cicd.git", branch: "master"
				sh "echo Cloning Done"
			}
		}
		stage("Build"){
			steps{
				docker build -t node-ToDo-app .
				sh "echo Build Done"
			}
		}
		stage("Scan"){
			steps{
				sh"echo Scanning Done"
			}
		}
		stage("Push Image"){
			steps{
				withCredential([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
					sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
					sh "echo Docker Login Success"
					sh "docker push ${env.dockerHubUser}/node-ToDo-app:latest"
					sh "echo Docker Push Done"
				}
			}
		}
		stage("Deploy"){
			steps{
				sh "docker-dompose down && docker-compose up -d"
				sh "Deployment Successful!"
			}
		}
	}
}
