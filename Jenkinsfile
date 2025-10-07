pipeline {
    agent any

    environment {
        SF_CONSUMER_KEY = credentials('SALESFORCE_CONSUMER_KEY')
        SF_USERNAME = 'venkatarao1411768@agentforce.com'
        SF_LOGIN_URL = 'https://login.salesforce.com'
        JWT_KEY_FILE = credentials('SALESFORCE_SERVER_KEY') // Jenkins file credential (private key)
        SFDX_CLI = 'C:\Program Files\sf\bin\sfdx' // Adjust path as needed
    }

    stages {
        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

        stage('Authorize Salesforce Org via JWT') {
            steps {
                sh "$sfdx force:auth:jwt:grant --clientid 3MVG9dAEux2v1sLvkZuaCg5KeC1I82ApE4_xEStysjgftuu2eG4cGziaxOcYh.SWuhCN7WCkEEtSSQGqhWI3A --jwtkeyfile C:\openssl\bin\server.key --username venkatarao1411@gmail.com --instanceurl https://login.salesforce.com --setdefaultdevhubusername"
            }
        }

        stage('Create Scratch Org') {
            steps {
                sh "${SFDX_CLI} force:org:create -f config/project-scratch-def.json -a test_scratch -s"
            }
        }

        stage('Push Source to Scratch Org') {
            steps {
                sh "${SFDX_CLI} force:source:push -u test_scratch"
            }
        }

        stage('Run Apex Tests') {
            steps {
                sh "${SFDX_CLI} force:apex:test:run -u test_scratch --wait 10"
            }
        }
 stages {
        stage('Demo: Modify XML false → true') {
            steps {
                script {
                    // Demo XML file path
                    def xmlFile = "Security.settings-meta.xml"

                    // Create a sample XML file for demo
                    writeFile file: xmlFile, text: """
                    <config>
                        <enableLogin>false</enableLogin>
                        <enableAdminAccess>false</enableAdminAccess>
                        <secureMode>true</secureMode>
                    </config>
                    """

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
   stage('Deploy to Staging/Production') {
            steps {
                input "Proceed to deploy to destination org?"
                sh "${SFDX_CLI} force:source:deploy -u DEST_ORG_ALIAS -p force-app/"
            }
        }
    }

    post {
        always {
            sh "${SFDX_CLI} force:org:delete -u test_scratch --noprompt"
        }
    }
}
}
