pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from your repository
                // For example, if using Git:
              https://github.com/muraliv21/MyWarehouse-dotnetcor6.git
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                // Navigate to the workspace directory
                script {
                    def workspaceDir
                    if (isUnix()) {
                        workspaceDir = sh(script: 'pwd', returnStdout: true).trim()
                    } else {
                        workspaceDir = bat(script: 'echo %WORKSPACE%', returnStatus: true).trim()
                    }

                    // Run the .NET Core 6 build command using the full path to 'dotnet'
                    def dotnetPath = "C:\\Program Files\\dotnet\\dotnet.exe"  // Update with the actual path
                    bat "cd ${workspaceDir}"
                    bat "\"${dotnetPath}\" build -c Release"
                }
            }
        }
    }
    
    post {
        success {
            // Archive your build artifacts if needed
            archiveArtifacts artifacts: '**/bin/**', allowEmptyArchive: true
        }
    }
}
