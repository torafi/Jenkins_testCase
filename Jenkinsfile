pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building..'
		bat 'java -version'
      }
    }
    stage('SIT') {
      steps {
	    echo 'Deploying to SIT env'
		bat 'E:\Sample_Code\deploy_to_tomcat.bat'	    	  
        echo 'Testing..'
      }
    }
    stage('Deploy to UAT') {
      steps {
        echo 'Deploying....'
      }
    }
	stage ('approval') {
		
		steps {
        echo 'Send approval email....'
      }
		}
	stage('Deploy to prod') {
	when {
	expression {
		currentBuild.result == null || currentBuild.result == 'SUCCESS' 
		}
		}
	steps {
  echo 'publish'
}
}	
  }
}
