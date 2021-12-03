pipeline {
    /* Define RE-USABLE variables */
    environment {
        /* IMAGE NAME tobe Build and push */
        registry = "unlimited.azurecr.io/sample-aspnet"
        /* Registry Credentials
         Manage Jenkins > Manage Credentials > Click on "Jenkins" Under "Store" > Global Credentials 
         Click "Add Credentials" link on left side panel
         Provide username, password and ID="reg_cred" */
        registryCredential = 'docker'
    }
   
    agent any
    
    stages {
        
        stage('Pull Source'){
            steps {
                git "https://github.com/mahendra-shinde/asp.net-core-ci"
            }
        }
        stage('Building image') {
            steps{
                script {
                    /* Use variable define on line#5 */
                    image = docker.build registry + ":$BUILD_NUMBER"                    
                }
            }
        }
        stage('Push to ACR'){
            steps{
                script{
                    /* Use the Credentials defined on line#10 */
                    docker.withRegistry('',registryCredential){
                        /* Image built on line#28 */
                        image.push()
                    }
                }
            }
        }
    }
}
