#!/usr/bin/env groovy
// shebang tells most editors to treat as groovy (syntax highlights, formatting, etc)

pipeline {

    agent any

    // Set Trigger mode: run every minutes
    triggers {
      pollSCM('* * * * *')
    }

    stages {
        // implicit checkout stage

        // On the server:
        // 1. use specific java version
        // 2. use specific maven version
        // 3. run common maven goals
        stage('Build') {
            steps {
                sh """JAVA_HOME=/usr/local/java/jdk-11.0.2 PATH=\$JAVA_HOME/bin:\$PATH
                      mvn clean install """
            }
        }
    }

    // post after stages:
    // for entire pipeline
    // an implicit step albeit with explicit config here, unlike implicit checkout stage
    post {
        always {
            // junit '**/target/surefire-reports/TEST-*.xml'
            // archiveArtifacts 'target/*.jar'
            archiveArtifacts 'retail_experience_client/target/*.jar'
        }
    }
}
