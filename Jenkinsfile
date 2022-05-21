pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId() 
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
     // Stage3 : Publish the artifacts to NEXUS
        stage ('Publish to Nexus'){
            steps {
                    script {

                def NexusRepo = Version.endsWith("SNAPSHOT") ? "GEL-Devopslab-SNAPSHOT" : "GEL-Devopslab-RELEASE"
                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: '7f6e0c41-f168-412d-8333-54d6827e1e5c', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.217:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
            }
            }
        }
      // Stage4 : Printing some information
      stage ('print some information'){
           steps{
               echo "Artifact ID is '${ArtifactId}'"
               echo "Version is '${Version}'"
               echo "GroupID is '${GroupID}'"
               echo "Name is '${Name}'"
           }
      } 
      // Stage5 : Deploying
        stage ('Deploy'){
            steps {
                echo ' deploying......'

            }
        }
     }
}