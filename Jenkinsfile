pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Black Duck Scan') {
            steps {
                script {
                    // Perform the Synopsys Black Duck scan 
                    def scanResults = synopsysSecurityScan(
                        scanType: 'BLACKDUCK',
                        blackDuckInstallation: 'BD-PARTNER',
                        failBuildForPolicyViolations: false,
                        publishResults: true
                    )
                    
                    // Get scan status and violations
                    def scanStatus = scanResults.getScanStatus()
                    def violations = scanResults.getPolicyViolations()
                    
                    // Format a comment with the scan results
                    def comment = "Black Duck Scan Results: Status - ${scanStatus}\n"
                    comment += "Policy Violations:\n"
                    violations.each { violation ->
                        comment += "- ${violation.policyName}: ${violation.description}\n"
                    }
                    
                    // Post the comment to the GitHub PR
                    githubPrComment(
                        context: "Black Duck Security Scan",
                        message: comment
                    )
                }
            }
        }
    }
}
