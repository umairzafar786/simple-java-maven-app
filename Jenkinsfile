pipeline {
    parameters {
        booleanParam (
            defaultValue: true,
            description: 'Artifact',
            name: 'CLICK_TO_PROCEED')
        booleanParam (
            defaultValue: false,
            description: 'No Artifact',
            name: 'CLICK_TO_PROCEED')
    }
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
    post {
        always {
            script {
            if ( params.CLICK_TO_PROCEED == true ) {
                archiveArtifacts artifacts: '/target/*.jar', onlyIfSuccessful: true 
            }
            else ( params.CLICK_TO_PROCEED == false) {
                bat echo "pipeline completed"
       }
      }          
    }
  }
}
