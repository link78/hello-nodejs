pipeline {
  agent any
  environmnent {
  dockerImage= ''
  }
  
  stages{
     stage ('Build Nodejs app') {
     steps {
     
     sh label: '',script: 'npm install'
     
     }
}
  
      stage('Buildgin Nodejs App Image Container'){
        when {
        branch 'master'
        }
        steps{
         script{
         dockerImage = docker.build("burk1212/hello-nodejs:${env.BUILD_NUMBER}")
         dockerImage.inside {
          sh 'echo $(curl localhost:9090)'
         }
         
        } // end of script
        }
      }
      
     stage('Push Image to Docker Hub'){
      steps {
        when { branch 'master'}
        script {
        docker.withRegistry('https://registry.hub.docker.com','Burk1212') {
          dockerImage.push("${env.BUILD_NUMBER}")
          dockerImage.push("latest")
        }
        }
      }
     }
    stage('Deploying') {
    steps {
      sh label: '',script: 'echo "deploying app"'
    }
    }
    
  } //end of stages
}