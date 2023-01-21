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
        sh '''./mvnw clean package -e && ./mvnw sonar:sonar \\
  -Dsonar.projectKey=pet-clinic \\
  -Dsonar.host.url=http://10.10.10.54:9000 \\
  -Dsonar.login=sqp_22f7838d38a8c5242a7ffee149d8b214324540b2'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh './mvnw spring-boot:run </dev/null &>/dev/null &'
          }
        }

        stage('Integration and Load Test') {
          steps {
            sh './mvnw verify'
            junit '**/target/surefire-reports/TEST-*.xml'
            perfReport ' **/target/jmeter/results/*'
          }
        }

      }
    }

  }
}