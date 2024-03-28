pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        jdk "JDK11"
        maven "Maven"
    }
    
    stages {
     stage('Build') {
            steps {
                bat 'mvn clean install -DskipTests=true'
            }
        }
    }
}
