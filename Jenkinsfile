pipeline {
    agent any

    stages {
        stage('Modify XML: false → true') {
            steps {
                script {
                    def xmlFile = "sample.xml"

                    // Create sample XML
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

                    echo "=== Original XML ==="
                    bat "type ${xmlFile}"

                    // Read and update XML
                    def xmlText = readFile(xmlFile)
                    def updatedXml = xmlText.replaceAll('>true<', '>false<')

                    // Save updated XML
                    writeFile file: xmlFile, text: updatedXml

                    echo "=== Updated XML ==="
                    bat "type ${xmlFile}"
                }
            }
        }
    }
}
