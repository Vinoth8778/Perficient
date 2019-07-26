pipeline {
    agent {
        node {
            ws("D:\Jenkins") {
                echo "awesome commands here instead of echo"
            }
        }
    }
             tools {
        maven 'maven'
        jdk 'java'
    }

    stages {
        stage('Clean-workspace') {
            steps {
                cleanWs()
            }
        }
        stage('src-checkout') {
            steps {
                git branch: 'master',
                //credentialsId: '12345-1234-4696-af25-123455',
                url: 'https://github.com/Vinoth8778/Perficient.git'
            }
        }
        /* stage('Deploy') {
            steps {
                    //bat 'mvn clean install'
                    /* rtMavenRun (
                     pom: 'pom.xml', goals: 'clean install',
                     deployerId: 'deployer-unique-id'
                    ) 
                    rtMavenDeployer (
                     id: 'deployer-unique-id',
                     serverId: 'Artifactory-1',
                     releaseRepo: 'libs-release-local',
                     snapshotRepo: 'libs-snapshot-local'
                    ) 
            } 
        } */
             stage('Jfrog-server') {
            steps {
                   rtServer (
                       id: "Artifactory-1",
                       url: "http://localhost:8081/artifactory",
                       // If you're using username and password:
                       //username: "admin",
                       //password: "password"
                       // If you're using Credentials ID:
                       credentialsId: 'Jfrog'
                       // If Jenkins is configured to use an http proxy, you can bypass the proxy when using this Artifactory server:
                       //bypassProxy: true
                       // Configure the connection timeout (in seconds).
                        //The default value (if not configured) is 300 seconds:
                        //timeout = 300
                       )
                }
            }
                stage('Jfrog-Deployer') {
                    steps {
                      rtMavenDeployer (
                        id: "deployer",
                        serverId: "Artifactory-1",
                        releaseRepo: "maven-release-local",
                        snapshotRepo: "maven-snapshot-local"
                        )
                 }
            }
            stage('Jfrog-MavenRun') {
                steps {
                     rtMavenRun (
                        pom: 'pom.xml', goals: 'clean install',
                        deployerId: "deployer"
                      )
                }
            }
            stage('Jfrog-Publish') {
                steps {
                    rtPublishBuildInfo (
                        serverId: "Artifactory-1"
                      )
                 }
            } 
                                        
                                        
                   }
    }
