pipeline {
  agent any

  stages {
    stage('Preparation') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker image') {
      steps {
        sh 'docker build . -t mohamedmamdouhiv/djangoapp:v1.0 --network host '
      }
    }

    stage('Push image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'my_user', passwordVariable: 'my_pass')]) {
          sh "docker login -u ${my_user} -p ${my_pass}"
          sh "docker push mohamedmamdouhiv/djangoapp:v1.0"
        }
      }
    }

    stage('Deploy') {
      steps {
        sh "kubectl apply -f /var/jenkins_home/workspace/test/app.yaml"
      }
    }
  }
}
