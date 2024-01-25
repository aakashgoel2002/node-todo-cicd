pipeline{
	
	agent {label "agent"}

	stages{
		stage("Code"){
			steps{
				git url: "https://github.com/aakashgoel2002/node-todo-cicd.git", branch: "master"
				sh "echo Cloning Done"
			}
		}
		stage("Build"){
			steps{
				sh "docker build -t node-todo-app ."
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
				withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
					sh "docker tag node-todo-app ${env.dockerHubUser}/node-todo-app"
					sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
					sh "echo Docker Login Success"
					sh "docker push ${env.dockerHubUser}/node-todo-app:latest"
					sh "echo Docker Push Done"
				}
			}
		}
		stage("Deploy"){
			steps{
				sh "docker-compose down && docker-compose up -d"
				sh "echo Deployment Successful!"
			}
		}
	}
}
