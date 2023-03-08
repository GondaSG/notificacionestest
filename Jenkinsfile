

pipeline {
	agent any
	
	parameters {
        booleanParam(name: 'REDEPLOY', defaultValue: false)
    }

    environment {
        SRC_PROJECT 	= 'notificacionestest'
        SRC_REPO_URL 	= "https://github.com/GondaSG"
        SVC_FOLDER		= 'desa'
        SVC_NAME		= 'vuce-notificaciones-api-app'
        ENVIRONMENT 	= 'desarrollo'
        BRANCH 			= 'main'
		REGISTRY_SERVER = "${REGISTRY_OCP_DEV_SERVER}"
		CLUSTER_NAME    = 'openshift_desa'
		PROJECT_NAME    = 'TBD'    
    }
    stages {

    	stage ('Prepare') {
            steps {
				script {
					checkoutGit( kind: 'proyect', repository: SRC_REPO_URL,
							     source: SRC_PROJECT, branch: BRANCH ) 
				}	
            }
        }

        stage ('Build') {
            steps {
				script {
					gradle(kind:'build',version:'8-jdk11',source: SRC_PROJECT) 
				}	
            }
        }

    }
	post {
	    always {
		    cleanWs()
	    }
    }
}
