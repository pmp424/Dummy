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

    // Load the file 'externalMethod.groovy' from the current directory, into a variable called "externalMethod".
    def externalMethod = load("externalMethod.groovy")

    // Call the method we defined in externalMethod.
    externalMethod.lookAtThis("Steve")

    // Now load 'externalCall.groovy'.
    def externalCall = load("externalCall.groovy")

    // We can just run it with "externalCall(...)" since it has a call method.
    externalCall("Steve")
}




