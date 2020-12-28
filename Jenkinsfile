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
                script{
                    def mavenPom = readMavenPom file: 'pom.xml'
                    def nexusVersion = mavenPom.version.endsWith("snapshot") ? "simple-app-snapshot" : "simple-app-release"
                 nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: "target/simple-app-${mavenPom.version}.war", 
                        type: 'war'
                    ]
                ], 
                        credentialsId: 'nex', 
                        groupId: 'in.javahome', 
                        nexusUrl: '172.31.8.78:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: "${nexusVersion}", 
                        version: "${mavenPom.version}"

                }
                
            }
        }
    }
}
