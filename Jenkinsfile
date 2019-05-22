pipeline { 
    agent any
	tools { 
        maven 'maven3.6.1' 
        jdk 'jdk8' 
    }
    stages {
		
		stage ('Build') {
            steps {
				dir('TestTodosServices') {
                    sh 'mvn clean install' 
                } 
            }
            post {
                success {
                    echo 'This is success build' 
                }
            }
        }
		
		stage ('Deploy') {
            steps {
				script {
					properties([
						parameters([
							string(name: 'DEPLOY_SERVER_URL', defaultValue: 'https://localhost:9443'),
							string(name: 'DEPLOY_SERVER_USER', defaultValue: 'admin'),
							password(name: 'DEPLOY_SERVER_PASSWORD', defaultValue: 'admin')
						])
					])
				}
				dir('TestTodosServicesCompositeApplication') {
                    sh 'mvn clean deploy -Dmaven.deploy.skip=true -Dmaven.car.deploy.skip=false -DserverUrl=${DEPLOY_SERVER_URL} -DserverUser=${DEPLOY_SERVER_USER} -DserverPassword=${DEPLOY_SERVER_PASSWORD}' 
                } 
            }
            post {
                success {
                    echo 'This is success deploy' 
                }
            }
        }
    }
}



