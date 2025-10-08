pipeline {
    agent any
    stages {
        stage('Modify XML: false → true') {
            steps {
                script {
                    // File name
                    def xmlFile = "Security.settings-meta.xml"
                    // Create sample XML file
             writeFile file: xmlFile, text: '''<config>
    <enableAccountHistoryTracking>true</enableAccountHistoryTracking>
    <enableAccountInsightsInMobile>false</enableAccountInsightsInMobile>
    <enableAccountOwnerReport>false</enableAccountOwnerReport>
    <enableAccountTeams>false</enableAccountTeams>
    <enableContactHistoryTracking>true</enableContactHistoryTracking>
    <enableRelateContactToMultipleAccounts>true</enableRelateContactToMultipleAccounts>
    <showViewHierarchyLink>true</showViewHierarchyLink>
</config>
'''
                    // Print original XML
                    echo "=== Original XML ==="
                    sh "cat ${xmlFile}"

                    // Read XML content
                    def xmlText = readFile(xmlFile)

                    // Replace all >false< with >true<
                    def updatedXml = xmlText.replaceAll('>false<', '>true<')

                    // Write updated XML back to file
                    writeFile file: xmlFile, text: updatedXml

                    // Print updated XML
                    echo "=== Updated XML ==="
                    sh "cat ${xmlFile}"
                }
            }
        }
    }
}
