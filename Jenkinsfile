node {
  try {
    stage('Checkout') {
        checkout scm
    }
    stage('Environment') {
        sh 'git --version'
        echo "Branch: ${env.BRANCH_NAME}"
        sh 'docker -v'
        
        try{
            sh "docker ps --filter name=counter-app-${env.BRANCH_NAME} -qa | xargs docker rm -f"
        }
        catch(Exception){
            echo "Remaining containers:"
            "sh docker ps --filter name=counter-app-${env.BRANCH_NAME} -qa"
        }
        
        sh 'printenv'
    }
    stage('Build Docker'){
        sh "docker build -t counter-app-${env.BRANCH_NAME} --label ${env.BRANCH_NAME} ."
    }
    stage('Deploy'){
        sh "docker run --publish-all=true -d -e VIRTUAL_HOST=${env.BRANCH_NAME} --name counter-app-${env.BRANCH_NAME} counter-app-${env.BRANCH_NAME}"
    }
  }
  catch (err) {
    throw err
  }
}