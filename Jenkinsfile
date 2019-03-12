pipeline {
  agent any
  triggers { 
  pollSCM('H */4 * * 1-5')
  }
  parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')

        file(name: "FILE", description: "Choose a file to upload")
    }
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
		bat 'E:\\Sample_Code\\deploy_to_tomcat.bat'	    	  
        echo 'Testing..'
      }
    }
	stage ("Different Test stages"){
	
	parallel {
                stage('Branch A') {
                    agent {
                        label "for-branch-a"
                    }
                    steps {
                        echo "On Branch A"
                    }
                }
                stage('Branch B') {
                    agent {
                        label "for-branch-b"
                    }
                    steps {
                        echo "On Branch B"
                    }
                }
                stage('Branch C') {
                    agent {
                        label "for-branch-c"
                    }
                    stages {
                        stage('Nested 1') {
                            steps {
                                echo "In stage Nested 1 within Branch C"
                            }
                        }
                        stage('Nested 2') {
                            steps {
                                echo "In stage Nested 2 within Branch C"
                            }
                        }
                    }
                }
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

stage('Example') {
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
            }
        }
  }
}
