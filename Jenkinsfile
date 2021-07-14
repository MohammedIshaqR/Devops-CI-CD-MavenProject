pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the artifacts to nexus 
        stage ('Publish to Nexus') {
            steps { 
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/com.vinaysdevopslab-0.0.8.war', type: 'war']], credentialsId: 'c783a82a-0399-4de3-a7ce-21b621740bf1', groupId: 'com.vinaysdevopslab', nexusUrl: '54.152.110.48:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'DevopsLab-SnapShot', version: '0.0.8'
            }
        }

        // Stage3 : Publish the source code to Sonarqube
        stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                     sh 'mvn sonar:sonar'
                }

            }
        }

        
        
    }

}
