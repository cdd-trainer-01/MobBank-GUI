pipeline {
    
    agent {
        label "master"
	}
    stages {
        stage("Export Porject") {
            steps {
             echo '**** mvn Build****'
			}
        }
        stage("Zip Project") {
            steps {
                echo '**** mvn Build****'    
            }
        }
        stage("Publish to Nexus") {
            steps {
			  echo "*** nexusVersion*****"       
			}
		}
	}		
    post { 
		always { 
			echo '----------Sending Build Notification to CDD--------------',
			env.GIT_REPO_NAME = env.GIT_URL.replaceFirst(/^.*\/([^\/]+?).git$/, '$1')

		}
		success { 

			withCredentials([string(credentialsId: 'CDD-Project-Mobile', variable: 'CDD_APIKEY')]){
	                	
				sendNotificationToCDD appName: "${env.GIT_REPO_NAME}" , 
					appVersion:  "${env.BRANCH_NAME}", 
					gitCommit: "${env.GIT_COMMIT}",
					gitPrevSuccessfulCommit: "${env.GIT_PREVIOUS_SUCCESSFUL_COMMIT}",
					overrideCDDConfig: [
						customApiKey: "${CDD_APIKEY}",
							customProxyPassword: '',
                            				customProxyUrl: '',
                           				customProxyUsername: '',
                            				customServerName: 'lvntest002908.bpc.broadcom.net',
                            				customServerPort: 8080,
                            				customTenantId: '00000000-0000-0000-0000-000000000000',
                            				customUseSSL: false
                    			],
					releaseTokens: '{}'
			}	
		}
	}
}
