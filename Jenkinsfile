pipeline{
    agent any

    stages{

        stage('Installing Dependencies'){

            steps {

                script {
                def nodejsTool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                env.PATH = "${nodejsTool}/bin:${env.PATH}"
                }

                sh 'echo "Building Dependencies..."'
                sh 'npm install'

            }
        }

        stage('Build Optimized React Production Files'){

            steps{

                sh 'echo "Building optimized react production files..."'
                sh 'npm run build'
            
            }
        }
    }
}