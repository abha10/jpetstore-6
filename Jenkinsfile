pipeline {
    agent any
    environment {
        test_result = ""
    }
    tools {
        maven 'maven3' 
    }
    stages {
        stage('Build & Test'){
          steps{
           sh 'mvn clean install'
        //   sh 'mvn cargo:run -P tomcat90'
          }
        }
       /* stage('Test') {
            steps {
             //   sh 'mvn test -P itest'
                script {
                    if ("${params.request_item_number}") {
                        test_result = "success";
                    }
                }
                echo "Building ..."
            }
        }*/
    }
    post {
        success {
            script{
                test_result = "success"
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
            echo "I failed"
            script{
                test_result = "failure"
                echo test_result
            }
        }
        always{
            script{
                echo "I' in always"
                echo test_result
            }
        }
    }
}
