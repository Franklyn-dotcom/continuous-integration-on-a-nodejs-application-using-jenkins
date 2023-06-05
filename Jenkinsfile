pipeline {
    agent any

    stages {
        stage("build") {
	   steps {
		echo "Bulding the application ..."
	   }      
        }
        
	stage("test"){
	    steps {
		echo "Testing builds ..."
		withCredentials([usernamePassword(credentialsId: 'dockerhub-credential', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
	             sh 'docker build -t franklyn27181/my-devops-projects docker/'
		     sh "echo $PASS | docker login -u $USER --password-stdin"
		     sh 'docker push franklyn27181/my-devops-projects:1.0'  
		}
	    }
	}
    }
    post {
	always {
	  echo "Checking application integration test...."
	}
	success {
	  echo "Succesfully built"
	  echo "Logging out of the container registry"
	  sh 'docker logout'
	}
    }
}
