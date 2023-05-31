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
        SONARSERVER ='sonar4.7'
        SONARSCANNER= 'sonar4.7'
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
        
        stage('CODE ANALYSIS with SONARQUBE') {
          
		  environment {
             scannerHome = tool "${SONARSCANNER}"
          }

          steps {
            withSonarQubeEnv("${SONARSERVER}") {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile-repo \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
          
              }
          }
        }
    }
}
