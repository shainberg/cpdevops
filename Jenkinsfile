pipeline {
    agent { 
        dockerfile true
    }
    stages {
        stage('build') {
            steps {
                script(
                    docker.build("counter-app-${env.BRANCH_NAME}")
                )
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

