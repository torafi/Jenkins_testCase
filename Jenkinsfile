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
		
	        bat  'copy C:\Users\Hp PC\Desktop\sample.war E:\Education\Tomcat\apache-tomcat-9.0.16-windows-x64\apache-tomcat-9.0.16\webapps\'
		bat  'E:\Education\Tomcat\apache-tomcat-9.0.16-windows-x64\apache-tomcat-9.0.16\bin\shutdown.bat'
		bat  'timeout 60'
		bat  'E:\Education\Tomcat\apache-tomcat-9.0.16-windows-x64\apache-tomcat-9.0.16\bin\startup.bat'
		bat  'timeout 60'
		  
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
