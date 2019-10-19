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
            sh "curl -u $JENKINS_CLI_USR:$JENKINS_CLI_PSW --silent ${BUILD_URL}api/json -o build.json"
            sh "cat build.json"  
          }
      }
    }
  }
}
