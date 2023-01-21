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
        sh '''./mvnw clean install -e && ./mvnw sonar:sonar \\
  -Dsonar.projectKey=pet-clinic \\
  -Dsonar.host.url=http://10.10.10.54:9000 \\
  -Dsonar.login=sqp_22f7838d38a8c5242a7ffee149d8b214324540b2'''
      }
    }

  }
}