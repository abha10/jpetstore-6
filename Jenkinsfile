pipeline {
 agent any

 tools {
  // maven 'mvn' 
  maven 'maven3'
 }
 stages {
  stage('Build & Test') {
   steps {
    sh 'mvn clean'
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
       	script{
       		 httpRequest authentication: 'snow-credential-id', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=SUCCESS&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"
       		}
       				
       	}
       	failure {
       	   script{
		   def response = httpRequest authentication: 'jenkins-creds', ignoreSslErrors: true, url: 'http://34.248.134.77:8080/job/jetpetstore-pipleine/'+"${BUILD_NUMBER}"+'/consoleText';
		   println '+++++++++++++++++++++++++++++++++++++++++++++\n'+response.content;
		   def snow_post = httpRequest authentication: 'snow-credential-id', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, consoleLogResponseBody: true, requestBody:"${response.content}" ,url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=FAILURE&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"  
       		}
       	}
     }
   }
  }
 }
