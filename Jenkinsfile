pipeline {
	agent any
	options {
	skipDefaultCheckout()
	}
	tools {
	maven 'maven'
	}
	stages {
	stage ('Intitialize') {
	steps {
	sh '''
	echo "PATH = ${PATH}"
	echo "M2_HOME = ${M2_HOME}"
	'''
	}
	}
	stage("checout source") {
	steps {
	checkoutm scm
	}
	}
	stage ('Build') {
	when {
	expression {
	currentBuild.result == null || currentbBuild.result == 'success'
	}
	}
	steps {
	sh 'mvn -B clean compile'
	}
	}
	stage ('Test') {
	steps {
	sh 'mvn -B test'
	}
	}
}
post {
	always {
	echo "Build finished"
	}
	success {
	echo "Build Success"
	}
	failure {
	echo "Build failure"
	}
}
}
