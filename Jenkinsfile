node {
	stage "checkout scm"
	sh "rm -fr *"
	checkout scm
	stage "build"
	def dcBuild=docker.build("artifactory.adskengineer.net/zookeeper-ochopod-example:v1")
  	stage 'Upload'
  	dcBuild.push()
  	stage 'Publish to dev ENV'
  	docker.image('artifactory.adskengineer.net/ors-utils:v2').inside {
  		sh "cicd-cli publish -m ./appVersionManifest.yml"
  	}
}