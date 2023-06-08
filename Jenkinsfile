
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
	environment{
		dockerHome= tool "my-docker" //my-docker is the name we gave to the ddocker we added inside the jenkings tool
		mavenHome= tool "my-maven"   //my-maven is the name we gave to the maven we added inside the jenkins tool
		PATH= "$dockerHome/bin:$mavenHome/bin:$PATH" //we are taking the dockerHome and mavenHome bins and adding them to the jenkins path
	}

	stages{
		stage ("Checkout"){
			steps{
				sh "mvn --version"
				sh "docker version"
				echo "Build"
				echo "build path is $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "build name is $env.JOB_NAME"
				echo "build tag is $env.BUILD_TAG"
				echo "build url is $env.BUILD_URL"

			}
		}

		stage("Compile"){
			steps{
				sh "mvn clean compile"  //similaar to npm install
			}
		}

		stage("Test"){
			steps{
				sh "mvm test"
			}
		}
		stage("Integration Test"){
			steps{
				sh "mvm failsafe:integration-test failsafe:verify"
			}
		}

	// 	stage("Package"){
	// 		steps{
	// 			sh "mvm package -DskipTests" //to create a jar file
	// 		}
	// 	}
		
	// 	stage("Build docker image"){
	// 		steps{
	// 			//THIS IS  THE SCRIPTIVE/OLD APPROACH
	// 			//"docker build -t in28min/currency-exchange-devops:$env.BUILD_TAG"

	// 			//THE NEW/DECLARATIVE APPROACH
	// 			script{
	// 				dockerImage=docker.build("gbambor/currency-exchange-devops:${env.BUILD_TAG}") //docker.build is used to build the docker image and the name dockerImagae is given to it to be able to referenceor call it somewhere else eg during the pushing
	// 			}
	// 		}
	// 	}

	// 	stage("Pushing Docker Image"){
	// 		steps{
	// 			script{
	// 				docker.WithRegistry("", "dockerhub") //to connect the credentials called dockerhub that we created in the jenkins ui to provide our username and password for docker hub
	// 				dockerImage.push()
	// 				dockerImage.push("latest")
	// 			}
	// 		}
	// 	}
	// }


	
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


