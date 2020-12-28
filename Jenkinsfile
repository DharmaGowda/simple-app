pipeline {
    agent any
    tools {
      maven 'maven3'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 // archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload artifacts to Nexus'){
            steps{
                 nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: 'target/simple-app-1.0.0.war', 
                        type: 'war'
                    ]
                ], 
                        credentialsId: 'nex', 
                        groupId: 'in.javahome', 
                        nexusUrl: '172.31.8.78:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'http://52.66.250.224:8081/repository/simple-app-release/', 
                        version: '1.0.0'
            }
        }
    }
}
