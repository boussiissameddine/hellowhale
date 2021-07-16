pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/boussiissameddine/hellowhale.git', branch:'master'
      }
    }
    
      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("issambits/hellowhale:${env.BUILD_ID}")
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
                     docker.withRegistry('https://registry.hub.docker.com', 'issambits') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
    
             stage( ' Déployer l'application ' ) {
                     steps {
                             script {
                              kubernetesDeploy( configs : " hellowhale.yml " , kubeconfigId : " mykubeconfig " )
          
        }
      }
     }

    
  

  }

}
