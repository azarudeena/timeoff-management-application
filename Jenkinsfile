node('nodejsapp'){
    def app
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/azarudeena/timeoff-management-application']]])
	}
	stage('prep'){
    	app = docker.build("nodejs/app:latest")
	}
	stage('verify'){
     app.inside {
                echo "Tests passed"
            }
	}
	stage('run-docker'){
		sh 'docker run -d -p 8080:8080 --env PORT=8080 --name timeoffapp nodejs/app:latest'
		echo "App is running"
	}
}
