pipeline {
    agent { 
        dockerfile{
            additionalBuildArgs "--label counter-app-${env.BRANCH_NAME} -t counter-app-${env.BRANCH_NAME}:latest"
        } 
    }
    /*stages {
        stage('build') {
            steps {
                sh 'echo Shainberg'
            }
        }
	stage('Shainberg'){
	    steps {
	        sh 'echo Shainberg'
		    sh 'touch Shainberg'
	    }
	}
    }*/
}

