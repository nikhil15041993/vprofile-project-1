pipeline { 
    
	agent any
    tools {
        maven "vprofile-maven"

    }

    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "13.126.187.63:8081"
        NEXUS_REPOSITORY = "vprofile-release"
	    NEXUS_REPOGRP_ID    = "vprofile-group"
        NEXUS_CREDENTIAL_ID = "nexus-pass"
        ARTVERSION = "${env.BUILD_ID}"
    }
	
    stages{
        
        stage('BUILD'){
            steps {
                sh 'mvn -s settings.xml  -DskipTests install'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        // stage('unit test')
        // {
        //     steps{
        //          sh 'mvn test'
        //     }
        // }


    }


    


}
