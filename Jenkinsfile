pipeline {
    agent any
    parameters {
        
        choice(name: 'RGName', choices: ['Ingress', 'Transact'], description: 'RG')
        
        booleanParam(name: 'Delete', defaultValue: 'true', description: '')
    }
    
    environment {
       
       AZURE_SUBSCRIPTION_ID='4917809c-4753-4722-81bf-a1b4429fd9ca'
        AZURE_TENANT_ID='819948b9-e473-435d-b429-6f100444732f'
        
    }

    stages {
        stage('Example') {
            steps {
                   withCredentials([usernamePassword(credentialsId: 'myAzureCredential', passwordVariable: 'CLIENT_SECRET', usernameVariable: 'AZURE_CLIENT_ID')]) {
                            sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $CLIENT_SECRET -t $AZURE_TENANT_ID'
                       
                       //sh  'az group create --location westus --resource-group $RGName'
                       
                        }
            }
	  }
	  
	 
        stage ('Delete') {
         steps {
        script {
             //def delete = build.getEnvVars()["Delete"]
	
            if('$Delete')
		{
                Write-Output (params.$Delete)
		sh 'az group delete --name $RGName --yes'	
		}
		
	}
	 }
        }
    }
    
}
