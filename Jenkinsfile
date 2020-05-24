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
		echo 'Docker run here'
	}
}
