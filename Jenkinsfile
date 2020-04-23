  // Parameterized controller and validator files
  properties(
    [parameters([choice(choices: ["gslb-config-controller.yaml", "gslb-config-validator.yaml", "gslb-deployment-controller.yaml", "gslb-deployment-validator.yaml", "gslb-reflection-controller.yaml", "notification-controller.yaml", "project-controller.yaml", "project-validator.yaml", "route-controller.yaml", "route-validator.yaml", "cae-esp-pod-controller.yaml", "felix-stats-monitor.yaml", "splunk-index-validator.yaml"].join("\n"),
	description: 'controller and validator File which need to Deploy',
	name: 'controller and validator files')])])
	
	com.cwctravel.hudson.plugins.extended_choice_parameter.ExtendedChoiceParameterDefinition extendedChoiceParameterDefinition = new com.cwctravel.hudson.plugins.extended_choice_parameter.ExtendedChoiceParameterDefinition(
    "OPTION_NAME", // name
    "PT_CHECKBOX", // type
    "option1,option2,option3", // values
    null, // projectName
    null, // propertyFile
    null, // groovyScript
    null, // groovyScriptFile
    null, // bindings
    null, // groovyClasspath
    null, // propertyKey
    "option1,option2", // defaultValue
    null, // defaultPropertyFile
    null, // defaultGroovyScript
    null, // defaultGroovyScriptFile
    null, // defaultBindings
    null, // defaultGroovyClasspath
    null, // defaultPropertyKey
    null, // descriptionPropertyValue
    null, // descriptionPropertyFile
    null, // descriptionGroovyScript
    null, // descriptionGroovyScriptFile
    null, // descriptionBindings
    null, // descriptionGroovyClasspath
    null, // descriptionPropertyKey
    null, // javascriptFile
    null, // javascript
    false, // saveJSONParameterToFile
    false, // quoteValue
    10, // visible item count
    "Select your options", // description
    "," //multiSelectDelimiter
)

normalChoiceOptions = ["option1","option2"]

properties([
        parameters([
                choice(choices: normalChoiceOptions.join("\n"), description: 'Single select option', name: 'SOME_OPTION'),                
                extendedChoiceParameterDefinition
        ])
])
node {

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




