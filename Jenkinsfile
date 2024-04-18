pipeline {
	agent any
	
	parameters {
		booleanParam(defaultValue: true, description: 'Build SSIS', name: 'BUILD')
		booleanParam(defaultValue: false, description: 'Deploy SSIS', name: 'DEPLOY')
	}
	
	environment {
		SSISBuildPath="C:\\SSIS_DEV_OPS\\SSISBuild.exe"
		SSISDeployPath="C:\\SSIS_DEV_OPS\\ssisdeploy.exe"
		SOLUTION = "AUDIT_Import_ALL\\AUDIT_Import_ALL.dtproj"
	}
	
	stages {
		stage('Checkout') { 
			PrintStage()
			
			steps {			  
				echo 'step Git Checkout'			
				checkout scm
			}
		}
		
		stage('Build') { 
			when {
				expression { 
					return params.BUILD
				}
			}
			steps {
				PrintStage()
				echo "step Build Solution"
			}
		}
		
		stage('Deploy') { 
			when {
				expression { 
					return params.DEPLOY
				}
			}
			steps {
				PrintStage()
				echo "step Deploy Solution"
			}
		}
	}
	
	post {
		always {
			script {
				currentBuild.result = currentBuild.result ?: 'SUCCESS'
			}
		}
	}
}

void PrintStage(String text=""){
    text=="" ? println ('* '*10 + env.STAGE_NAME.toUpperCase() + " *"*10) : println (text)
}