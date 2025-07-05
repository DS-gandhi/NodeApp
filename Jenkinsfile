pipeline{
	agent any
	stage{

		stage("Build"){
				steps{
					echo "Start Building"
					sh "npm install"
					sh "npm run build"
					echo "Building success"
				}
			}
			
		}

}