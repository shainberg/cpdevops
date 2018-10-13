pipeline {
    agent { docker { image 'node:6.3' } }
    stages {
        stage('build') {
            steps {
                sh 'npm --version'
            }
        }
	stage('Shainberg'){
	    steps {
	        sh 'echo Shainberg'
	    }
	}
    }
}

