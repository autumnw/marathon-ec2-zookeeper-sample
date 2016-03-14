node {
	stage "checkout from scm"
	sh "rm -fr *"
	checkout scm
	stage "Build docker image"
	def dcBuild=docker.build("artifactory.adskengineer.net/zookeeper-ochopod-example:v1")
  	stage 'Push docker image'
  	dcBuild.push()
  	stage 'Deploy to dev ENV and publish'
  	docker.image('artifactory.adskengineer.net/ors-utils:v5').inside {
		sh "cicd-cli publish -m ./appVersionManifest.yml"
		sh "cicd-cli deploy -e Dev -r us-east -p mesos -a zookeeper-ochopod-example -v 1"
		sh "cicd-cli notify -e Dev -n zookeeper-ochopod-example -v 1"
  	}
}