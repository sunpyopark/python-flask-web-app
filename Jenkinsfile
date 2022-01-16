node {
    
    environment {
        SLACK_CHANNEL = '#jenkins-ci'
    }	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'krandmm/subserve-chatbot'
    def version = ':v0.1.'
    def awsecrCredential = 'dmg-ecr-credentials'
    def awsecrregistry = 'dmg-python-coreapp'
	
	stage('Git') {
		git 'https://github.com/sunpyopark/python-flask-web-app/'
	}

	stage('Building Docker image For AWS ECR') {
        docker.withRegistry('https://808066484529.dkr.ecr.us-west-1.amazonaws.com/dmg-python-coreapp/', 'ecr:us-west-1:dmg-ecr-credentials') {
	   def buildName = awsecrregistry + version + "$BUILD_NUMBER"
		newApp = docker.build buildName
		newApp.push()
        }
        }

        stage('Removing image') {
            sh "docker rmi $registry:$BUILD_NUMBER --force"
            sh "docker rmi $registry:latest --force"
        }
	stage("Slack speak") {
        slackSend color: '#BADA55', message: 'Hello, World!'
        }
}
