pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building..'
      }
    }
    stage('SIT') {
      steps {
        echo 'Testing..'
      }
    }
    stage('Deploy to UAT') {
      steps {
        echo 'Deploying....'
      }
    }
	
	stage('Deploy to prod') {
	when {
	expression {
		currentBuild.result == null || currentBuild.result == 'SUCCESS' ①
		}
		}
	steps {
	sh 'make publish'
}
}	
  }
}