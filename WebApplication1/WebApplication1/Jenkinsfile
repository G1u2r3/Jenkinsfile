pipeline {
    agent any

    environment {
        DOTNET_HOME = tool name: 'dotnet-sdk', type: 'com.cloudbees.jenkins.plugins.customtools.CustomTool'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://your-repo-url.git' // Replace with your repository URL
            }
        }
        stage('Restore') {
            steps {
                script {
                    withEnv(["PATH+DOTNET=${DOTNET_HOME}/bin"]) {
                        sh 'dotnet restore'
                    }
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    withEnv(["PATH+DOTNET=${DOTNET_HOME}/bin"]) {
                        sh 'dotnet build --configuration Release'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    withEnv(["PATH+DOTNET=${DOTNET_HOME}/bin"]) {
                        sh 'dotnet test'
                    }
                }
            }
        }
        stage('Publish') {
            steps {
                script {
                    withEnv(["PATH+DOTNET=${DOTNET_HOME}/bin"]) {
                        sh 'dotnet publish --configuration Release --output ./publish'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Example: Copy files to the deployment directory
                    sh 'cp -r ./publish/* /path/to/deploy'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/publish/**'
            junit '**/TestResults/*.xml'
        }
    }
}
