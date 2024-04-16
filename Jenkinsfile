pipeline { 
    
	agent any
    tools {
        maven "vprofile-maven"

    }

    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "13.126.187.63:8081"
        RELEASE_REPO = "vprofile-release"
	    NEXUS_GRP_REPO    = "vprofile-group"
        NEXUS_CREDENTIAL_ID = "nexus-pass"
        ARTVERSION = "${env.BUILD_ID}"
        NEXUSIP = "13.126.187.63"
        NEXUSPORT = "8081"
        SNAP_REPO = "vprofile-snapshot"
        CENTRAL_REPO = "vprofile-dependency"


    }
	
    stages{
        
        stage('BUILD'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('unit test')
        {
            steps{
                 sh 'mvn test'
            }
        }

        stage('INTEGRATION test')
        {
            steps{
                sh 'mvn verify -DskipUnitTests'
            }

        }
        stage('CODE ANALYSIS WITH CHECKSTYLE')
        {
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }


    }


    


}
