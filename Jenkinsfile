pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        jdk "JDK11"
        maven "Maven"
    }
    
    stages {
        stage('Get Code') {
            steps {
                git(
                   url: 'https://github.com/poc-synopsys/insecure-bank.git',
                   credentialsId: 'poc-synopsys',
                   branch: "main"
                )             
            }
        }
      stage('Coverity on Polaris') {
            steps {
                polaris arguments: 'analyze -w', polarisCli: 'Polaris - Demo'// Run Polaris (SAST) analysis
            }
        }
     stage('Análise Black Duck') {
            steps {
                synopsys_detect detectProperties: '', downloadStrategyOverride: [$class: 'ScriptOrJarDownloadStrategy'] // Run Black Duck (SCA) analysis
            }
        }        
    }
}
