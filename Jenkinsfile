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
		    script{
			    try{
		    		sh 'mvn test'
				def response = httpRequest authentication: 'snow-credential-id', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=SUCCESS&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"
			    }catch(e){
				   
    					//String error = "${e}";
					httpRequest authentication: 'snow-credential-id', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, consoleLogResponseBody: true, requestBody:"${e}" ,url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=FAILURE&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"  
	/*post {
	    success {
		script{
			 def response = httpRequest authentication: 'snow-credential-id', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=SUCCESS&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"
			}
					
		}
		failure {
		   script{
			httpRequest authentication: 'snow-credential-id', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, consoleLogResponseBody: true, requestBody:"${currentBuild.rawBuild.log}" ,url: 'https://dev39754.service-now.com/api/190726/snow_jenkins?status=FAILURE&request_item_number=' + "${params.Request_Item_Number}" + '&job_name=' + "${JOB_NAME}" + '&build_number=' + "${BUILD_NUMBER}"  
			}
		}
		}*/
        }
		    }
		}
    }
	}
}
