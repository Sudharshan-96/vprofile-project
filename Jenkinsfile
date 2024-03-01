pipeline {
    agent any
    tools {
        maven "maven3"
        jdk "OracleJDK17"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUS_IP = '34.168.247.18'
        NEXUS_PORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s pom.xml -DskipTests install'
            }
            post {
                success {
                    echo 'Archiving'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
            
        }
        stage('test') {
            steps {
                sh 'mvn -s pom.xml test'
            }
        }

        stage( 'checkstyle Analysis') {
            steps {
                sh 'mvn -s pom.xml checkstyle:checkstyle'
            }
        }
    }        
}
