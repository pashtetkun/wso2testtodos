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
				dir('TestTodosServicesCompositeApplication') {
                    sh 'mvn clean deploy -Dmaven.deploy.skip=true -Dmaven.car.deploy.skip=false -DserverUrl=https://localhost:9443 -DserverUser=admin -DserverPassword=admin' 
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



