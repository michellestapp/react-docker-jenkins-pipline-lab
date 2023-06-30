pipeline{
    agent any

    stages{

        stage('Installing Dependencies'){

            script {
                def nodejsTool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                env.PATH = "${nodejsTool}/bin:${env.PATH}"
            }

            sh 'echo "Building Dependencies..."'
            sh 'npm install'

        }
    }
}