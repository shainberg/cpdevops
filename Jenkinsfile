node {
  try {
    stage('Checkout') {
        checkout scm
    }
    stage('Environment') {
        sh 'git --version'
        echo "Branch: ${env.BRANCH_NAME}"
        sh 'docker -v'
       //def imagesToRemove = sh "docker images | grep counter-app-${env.BRANCH_NAME}"
        //echo "result: ${imagesToRemove}"
        //if (imagesToRemove != ''){
        //    echo "${imagesToRemove}"
        //    sh "docker rmi -f ${imagesToRemove}"
        //}
        dockerImages = "docker images".execute().text.split("/\n/")
        echo "${dockerImages}"
	    snapshotImages = dockerImages.findAll{ it.contains(env.BRANCH_NAME) || it.contains("<none>") }
        echo "${snapshotImages}"
	    snapshotImages.each {output -> println("docker rmi -f ${output.split()[2]}".execute().text)}
        dockerImagesAfter = "docker images".execute().text.split("/\n/")
        echo "${dockerImagesAfter}"
        try{
            sh "docker ps -aq --no-trunc -f status=exited | xargs docker rm"

            sh "docker images -q --filter dangling=true | xargs docker rmi"
        }
        catch(Exception e1){
            echo "Error removing containers"
        }


        sh 'printenv'
    }
    stage('Build Docker'){
        sh "docker build -t counter-app-${env.BRANCH_NAME} --label ${env.BRANCH_NAME} ."
    }
    stage('Deploy'){
        sh "docker run --publish-all=true -d -e VIRTUAL_HOST=${env.BRANCH_NAME} --name counter-app-${env.BRANCH_NAME} counter-app-${env.BRANCH_NAME}"
        sh "docker images -q --filter dangling=true | xargs docker rmi -f"
    }
  }
  catch (err) {
    throw err
  }
}