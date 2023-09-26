pipeline {
	agent any
	parameters {
		choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
		booleanParam(name: 'executeTests', defaultValue: true, description: '')
	}               
	stages {
		stage("build") {
			steps {
				echo "build"
			}
		stage("test") {
			when {
				expression {
					params.executeTests == true
				}
			}
			steps {
				echo "test"
			}
		stage("deply") {
			steps {
				echo "deploy"
				echo "deplying version ${params.VERSION}"
			}
		}
	}
}