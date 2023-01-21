pipeline {
  agent {
    node {
      label 'test'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw clean -e sonar:sonar \\
  -Dsonar.projectKey=pet-clinic \\
  -Dsonar.host.url=http://18.143.65.52:9000 \\
  -Dsonar.login=sqp_22f7838d38a8c5242a7ffee149d8b214324540b2'''
      }
    }

  }
}