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
                    docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
     }
}
