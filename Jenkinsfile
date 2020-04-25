node {
	  
	String[] ClusterValue= "${params.Cluster}".split(',');
	String[] PodsValue= "${params.Pod}".split(',');
  
    try{
	
		stage("Reading Cluster/Clusters"){
		println "Selected Cluster is ${ClusterValue}"
		}
		stage("Reading Common Yaml files"){
			sh '''
				echo "Below are the common files that are going to deploy for all PODs" > YamlFilesList.txt
				echo " " >> YamlFilesList.txt
				echo "felix-pull-creds.yaml" >> YamlFilesList.txt
				echo "gslb-admin.yaml" >> YamlFilesList.txt
				echo "cluster.yaml" >> YamlFilesList.txt
				echo "felix-process-ctrl.yaml" >> YamlFilesList.txt
				echo "acc-config.yaml" >> YamlFilesList.txt
				echo "felix-secret.yaml" >> YamlFilesList.txt
				echo "common-config-temp.yaml" >> YamlFilesList.txt
				echo "felix-stats-monitor.yaml" >> YamlFilesList.txt
				echo "old-rw-temp.yaml" >> YamlFilesList.txt
				echo " " >> YamlFilesList.txt
				echo "Along with above files, below yaml files also going to be deployed for selected POD/PODs" >> YamlFilesList.txt
				echo "The selected POD/PODs are: ${PodsValue}" >> YamlFilesList.txt
				echo " " >> YamlFilesList.txt
			'''
			println "Below are the common files from YamlFilesList file"
			sh "cat YamlFilesList.txt"
		}
		stage("Reading Pods and respective Yaml files"){
			println "PODs that are selected : ${PodsValue}"
		
			for (pn in PodsValue) {
				if (pn == "notification-controller") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-subscription.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "project-controller") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-felixproject.yaml" >> YamlFilesList.txt
						echo "crd-routestate.yaml" >> YamlFilesList.txt
						echo "crd-splunk-index.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "project-validator") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-gslb-deployment.yaml" >> YamlFilesList.txt
						echo "crd-felixproject.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "route-controller") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-certificate.yaml" >> YamlFilesList.txt
						echo "crd-routestate.yaml" >> YamlFilesList.txt
						echo "crd-gslb-config.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "route-validator") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-gslb-deployment.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "splunk-index-validator") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-splunk-index.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "felix-stats-monitor") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-certificate.yaml" >> YamlFilesList.txt
						echo "crd-routestate.yaml" >> YamlFilesList.txt
						echo "crd-gslb-config.yaml" >> YamlFilesList.txt
						echo "crd-gslb-deployment.yaml" >> YamlFilesList.txt
						echo "crd-felixproject.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "gslb-config-controller") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-gslb-config.yaml" >> YamlFilesList.txt
						echo "crd-reflection-request.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "gslb-config-validator") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-gslb-config.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "gslb-deploy-controller") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-certificate.yaml" >> YamlFilesList.txt
						echo "crd-gslb-config.yaml" >> YamlFilesList.txt
						echo "crd-gslb-deployment.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "gslb-deployment-validator") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-gslb-deployment.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
				if (pn == "gslb-reflection-controller") {
					sh '''
						echo "CRD files for ${pn}" >> YamlFilesList.txt
						echo "crd-reflection-request.yaml" >> YamlFilesList.txt
						echo "crd-gslb-deployment.yaml" >> YamlFilesList.txt
						echo " " >> YamlFilesList.txt
					'''
				}
			}
		
				println "Below are the actual Yaml files list respective to selected PODs"
				sh "cat YamlFilesList.txt"
				sh "uniq YamlFilesList.txt > UniqYamlFilesList.txt"
				println "Below are the yaml files that are going to be deployed"
				sh "cat UniqYamlFilesList.txt"
		}		
			
		stage("Deploy the pods"){ 
		
		}

	}
	catch (e){
		println "*** Badness: $e"
	}
}
