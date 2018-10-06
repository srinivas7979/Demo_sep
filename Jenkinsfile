pipeline {
    agent any 
    tools {
        maven 'MY_MVN'
    }
   
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage ('Clone repository') {
            steps {
            checkout scm
            }
        }
        stage('Build') {
            steps {
               echo "Hello this is jenkins pipeline"
               sh 'cd "${WORKSPACE}" && mvn -Dmaven.test.failure.ignore=true install' 
               
            }
        }
       sshagent(['tomcat_server_root']) {
    		sh 'scp "${WORKSPACE}/*.war" 192.168.33.20:/opt/apache-tomcat-8.5.32/webapps/'
	}
    }
}
