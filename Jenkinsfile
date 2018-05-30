pipeline {
    agent any
  
    tools {
       // maven 'mvn' 
        maven 'maven3' 
    }
    stages {
        stage('Build & Test'){
          steps{
           sh 'mvn clean'
           sh 'mvn compile'
        //   sh 'mvn cargo:run -P tomcat90'
          }
	}
	    stage('Test'){
		    steps{
		    sh 'mvn test'
		    }
	post {
	    success {
		script{
			 def response = httpRequest authentication: 'snow-credential-id', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=SUCCESS&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"
			}
					/*script {
						if (test_result == "success") {
							def response = httpRequest contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, requestBody: '${params.request_item_number}', url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=success&request_item_number=' + "${params.request_item_number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"
						} else {
							httpRequest contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, requestBody: '${params.request_item_number}', url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=failure&request_item_number=' + "${params.request_item_number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"
						}
					}*/
		}
		failure {
		   script{
			httpRequest authentication: 'snow-credential-id', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, consoleLogResponseBody: true, requestBody:"${currentBuild.rawBuild.log}" ,url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=FAILURE&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"  
			}
		}
		}
        }

    }
}
