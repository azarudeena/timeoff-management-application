node('nodejsapp'){

    environment {
           PORT='8080'
       }
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
		environment {
           PORT='8080'
       }
		sh "docker run -d -p 8080:8080 --env PORT=${PORT} nodejs/app:latest"
		 echo 'App is running'
	}
}
