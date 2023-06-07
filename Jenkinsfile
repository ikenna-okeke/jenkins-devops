
// SCRIPTED PIPELINE 
//a node refers to the machine where you run your pipeline, and a pipeline can be divided into different stages
//
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage("Integration Test"){
// 		echo "integration"
// 	}
// }


//DECLARATIVE APPROACH
//agent is where your pipeline will run, it is similar to node but gives you a lot of flexibility
pipeline {
	agent any
	
	// agent {docker{image "maven:3.6.3"}}
	stages{
		stage ("Build"){
			steps{
				//sh "mvn --version"
				echo "Build"
				echo "build path is $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "build name is $env.JOB_NAME"
				echo "build tag is $env.BUILD_TAG"
				echo "build url is $env.BUILD_URL"

			}
		}

		stage("Test"){
			steps{
				echo "Test"
			}
		}

		stage("Integration"){
			steps{
				echo "Integration"
			}
		}
	}
	
	post{ // post means after all the stages have been executed what should happen
		always{ //whether success or fail
			echo "i am awesome"
		}

		success{ //only on success
			echo "i run when you are succesful"
		}

		failure{//on failure
			echo "i run when you fail"
		}

		changed{ //for example executes when the pipeline status changes from failure to sucess or sucess to failure
			echo "I changed now haha"
		}
	}

	
	
}


