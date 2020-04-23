node {

  // Parameterized CRD files
  properties(
    [parameters([choice(choices: ["crd-certificate.yaml", "crd-felixproject.yaml", "crd-gslb-config.yaml", "crd-gslb-deployment.yaml", "crd-reflection-request.yaml", "crd-routestate.yaml", "crd-subscription.yaml", "crd-splunk-index.yaml"].join("\n"),
    description: 'CRD File which need to Deploy', 
    name: 'CRD_Files')])])

  // Parameterized controller and validator files
  properties(
    [parameters([choice(choices: ["gslb-config-controller.yaml", "gslb-config-validator.yaml", "gslb-deployment-controller.yaml", "gslb-deployment-validator.yaml", "gslb-reflection-controller.yaml", "notification-controller.yaml", "project-controller.yaml", "project-validator.yaml", "route-controller.yaml", "route-validator.yaml", "cae-esp-pod-controller.yaml", "felix-stats-monitor.yaml", "splunk-index-validator.yaml"].join("\n"),
	description: 'controller and validator File which need to Deploy',
	name: 'controller and validator files')])])
	
 	def PROJECT_NAME = "project_name"

    // Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
        	checkout scm
        }
        stage ('Build') {
        	sh "echo 'shell scripts to build project...'"
        }
        stage ('Tests') {
	        parallel 'static': {
	            sh "echo 'shell scripts to run static tests...'"
	        },
	        'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests...'"
	        }
        }
      	stage ('Deploy') {
            sh "echo 'shell scripts to deploy to server...'"
      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}




