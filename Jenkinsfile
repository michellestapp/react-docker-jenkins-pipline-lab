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

        stage('Build Docker Image') {

            steps {
                script {
                    def dockerTool = tool name: 'docker-latest-tool', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
                    env.PATH = "${dockerTool}/bin:${env.PATH}"
                }

                sh '''
                echo "Building Docker image..."
                docker build -t michellestapp/react-docker-jenkins-pipeline-lab:latest .
                '''
            }
        }

        stage('Push Docker Image to Docker Hub') {

            steps {

                withCredentials([usernamePassword(credentialsId:'personal docker credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
                    sh 'docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}'
                }
                
                sh'''
                echo "Pushing Docker image to Docker Hub..."
                echo $DOCKER_USERNAME
                docker --version
                '''
            }


        }
        }
    }
