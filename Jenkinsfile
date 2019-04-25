pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    label "jenkins-maven"
  }
  environment {
    DEPLOY_NAMESPACE = "catalog-service-prod"
  }
  stages {
    stage('Validate Environment') {
      steps {
        container('maven') {
          dir('env') {
            sh 'jx step helm build'
          }
        }
      }
    }
    stage('Update Environment') {
      when {
        branch 'catalog-service-prod'
      }
      steps {
        container('maven') {
          dir('env') {
            sh 'jx step helm apply'
          }
        }
      }
    }
  }
}
