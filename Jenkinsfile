pipeline {
    environment {
    registry = "umairzafar786/springdemo"
    registryCredential = 'dockerhub'
  }
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
    }
        stage('Build_image'){
            steps {
                script {
                    app = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
       stage('Image_Push') {
          steps {
              script {
                  docker.withRegistry( '', registryCredential ) {
                    app.push()
             }
          }
        }
     }
   stage('Remove Unused docker image') {
     steps {
           bat "docker rmi $registry:$BUILD_NUMBER"
     }
   }
}
    
}
