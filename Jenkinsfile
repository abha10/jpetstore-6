pipeline {
 agent any

 tools {
   maven 'mvn' 
//  maven 'maven3'
 }
 stages {
  stage('Build') {
   steps {
    sh 'mvn compile'
     //   sh 'mvn cargo:run -P tomcat90'
   }
  }
  stage('Test') {
   steps {
    sh 'mvn test'
   }
   post {
    success {
     script {
      httpRequest authentication: 'snow_auth', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, url: 'https://dev39754.service-now.com/api/x_ecsd_barclays_sn/jenkins_post?status=SUCCESS&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"
     }

    }
    failure {
     script {
      def response = httpRequest authentication: 'jenkins-creds', contentType: 'TEXT_PLAIN', ignoreSslErrors: true, url: 'http://jenkins.agile.env.ecs.digital/job/'+"${JOB_NAME}"+'/'+ "${BUILD_NUMBER}" + '/consoleText';

      def snow_post = httpRequest authentication: 'snow_auth', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, consoleLogResponseBody: true, requestBody: "${response.content}", url: 'https://dev39754.service-now.com/api/x_ecsd_barclays_sn/jenkins_post?status=FAILURE&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"
     }
    }
   }
  }
 }
}
