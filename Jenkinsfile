pipeline {
    agent { 
        dockerfile true
    }
    stages {
        stage('build') {
            steps {
                node{
                    docker.build("counter-app-${env.BRANCH_NAME}")
                }
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

