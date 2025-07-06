pipeline{
	agent any

	environment {
		EC2_USER = 'ubuntu'
		EC2_HOST = '13.232.37.137'
		SSH_CREDENTIAL_ID = 'ec2-ssh-key'
	}
	stages{

		stage("Build"){
				steps{
					echo "Start Building"
					sh "npm install"
					sh "npm run build"
					echo "Building success"
				}
			}
			stage("Deploy"){
				steps{
					echo "Starting Deployment on EC2"
					// use withCredentials to inject SSH private key
					sshagent(['ec2-ssh-key']){
						echo "copying build artifacts to EC2"
						scp '-o StrictHostCheckingKey=no -r dist/* ubuntu@13.232.37.137:/var/www/html'
						echo "Restarting web server on EC2"
						ssh '-o StrictHostCheckingKey=no ubuntu@13.232.37.137 'sudo systemctl restart nginx'
					}
					echo "Deployment completed"


				}

			}
		}

}