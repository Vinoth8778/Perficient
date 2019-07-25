pipeline {
    agent any
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
        stage('Deploy') {
            steps {
                    bat 'mvn clean install'
                    /* rtMavenRun (
                    pom: 'pom.xml', goals: 'clean install'
                ) */
            }
        }
        stage('Jfrog-Artifactory')
            steps {
                    rtServer (
                        id: "Artifactory-1",
                        url: "http://localhost:8081/artifactory",
                        // If you're using username and password:
                        username: "admin",
                        password: "password"
                        // If you're using Credentials ID:
                        credentialsId: 'Jfrog'
                        // If Jenkins is configured to use an http proxy, you can bypass the proxy when using this Artifactory server:
                        //bypassProxy: true
                        // Configure the connection timeout (in seconds).
                        // The default value (if not configured) is 300 seconds:
                        //timeout = 300
                        )
                    }
    }
}