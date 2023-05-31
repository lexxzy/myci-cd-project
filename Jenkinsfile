pipeline {
    agent any 
    tools {
        maven "MAVEN3"
        jdk "oracleJDK8"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        NEXUSIP = '172.31.20.67'
        NEXUSPORT= '8081'
        CENTRAL_REPO= 'vpro-maven-central'
        RELEASE_REPO= "vprofile-release"
	    NEXUS_GRP_REPO   = "vpro-maven-group"
        NEXUS_LOGIN = "nexuslogin"
    
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now Archiving"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }

        }

        stage('Test') {
            steps {
                sh 'mvn -s settings.xml test'

            }
        }

        stage ('Checkstyle Analysis') {
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }
    }
}
