library 'cb-days@master'
pipeline {
  agent { label'default-jnlp'}
  options { 
    buildDiscarder(logRotator(numToKeepStr: '4'))
    skipDefaultCheckout true
  }
  triggers {
    eventTrigger jmespathQuery("ref_type=='branch'")
  }
  stages {
    stage('Create Managed Master from Groovy') {
      when { 
        triggeredBy 'EventTriggerCause' 
        beforeAgent true
      }
      environment {
        JENKINS_CLI = credentials('cli-username-token')
      }
      steps {
          script {
              def eventTriggerCause = currentBuild.getBuildCauses()[0]
              echo $eventTriggerCause
          }
      }
    }
  }
}
