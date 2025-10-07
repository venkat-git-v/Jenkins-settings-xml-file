pipeline {
    agent any

    stages {
        stage('Demo: Modify XML false → true') {
            steps {
                script {
                    // Demo XML file path
                    def xmlFile = "Security.settings-meta.xml"

                    // Create a sample XML file for demo
                    writeFile file: xmlFile, text: """
                    <config>
                    <enableAccountHistoryTracking>true</enableAccountHistoryTracking>
                    <enableAccountInsightsInMobile>false</enableAccountInsightsInMobile>
                    <enableAccountOwnerReport>false</enableAccountOwnerReport>
                    </config>
                    echo "=== Original XML ==="
                    sh "cat ${xmlFile}"

                    // Replace all <tag>false</tag> with <tag>true</tag>
                    def xmlText = readFile(xmlFile)
                    def updatedXml = xmlText.replaceAll('>false<', '>true<')

                    // Write updated content back to file
                    writeFile file: xmlFile, text: updatedXml

                    echo "=== Updated XML ==="
                    sh "cat ${xmlFile}"
                }
            }
        }
    }
}
