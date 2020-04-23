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

    def server = Artifactory.newServer url: SERVER_URL, credentialsId: CREDENTIALS
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo

    stage ('Clone') {
        git url: 'https://github.com/jfrog/project-examples.git'
    }

    stage ('Artifactory configuration') {
        rtMaven.tool = MAVEN_TOOL // Tool name from Jenkins configuration
        rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
        rtMaven.resolver releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot', server: server
        buildInfo = Artifactory.newBuildInfo()
    }

    stage ('Exec Maven') {
        rtMaven.run pom: 'maven-example/pom.xml', goals: 'clean install', buildInfo: buildInfo
    }

    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }
}




