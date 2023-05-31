pipeline {
    agent any 
    tools {
        maven "MAVEN3"
        jdk "oracleJDK8"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_VERSION = "nexus3"
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        NEXUS_PROTOCOL = "http"
        NEXUSIP = '54.89.125.149'
        NEXUSPORT= '8081'
        CENTRAL_REPO= 'vpro-maven-central'
        RELEASE_REPO= "vprofile-release"
	    NEXUS_GRP_REPO   = "vpro-maven-group"
        NEXUS_LOGIN = "nexuslogin"
        ARTVERSION = "${env.BUILD_ID}"
    
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
        }
    }
}
