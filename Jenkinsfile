pipeline {
    agent { 
        dockerfile{
            label "counter-app-${env.BRANCH_NAME}"
        } 
    }
    stages {
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
    }
}

