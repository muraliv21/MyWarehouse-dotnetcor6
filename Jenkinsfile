pipeline {
    agent any
    
  // environment {
        // Use the globally defined .NET SDK location
       // DOTNET_ROOT = tool name:'netsdk6', type: 'sdk'
		
		//DOTNET_ROOT = netsdk6: 'DotNet', type: 'Tool'
		//PATH = "${tool name: 'sdk6', type: 'ToolInstallation'}/:${env.PATH}"
		//PATH = "${tool name: 'netsdk6', type: 'ToolInstallation'}/:${env.PATH}"
		 // .NET SDK = tool name: 'netsdk6', type: 'sdk'
		  // DOTNET_HOME = tool name: 'netsdk6', type: 'sdk'
          // DOTNET_ROOT = "${DOTNET_HOME}/.dotnet"
		  //DOTNET_ROOT = tool name: 'netsdk6' , type: 'sdk'
	   environment {
    // Set the path to the .NET SDK 6 installation
    PATH = "${tool name: 'netsdk6', type: 'SdkInstallation'}/bin:${env.PATH}"
}

		  



   // }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from your repository
                // For example, if using Git:
				http://vagit.vitalaxis.com/vitalaxis/CloudOps/dotnetcore6webapplinux.git
                checkout scm
            }
        }
        
        stage('Build and Publish') {
            steps {
                // Navigate to the workspace directory
                script {
                    def workspaceDir
                    if (isUnix()) {
                        workspaceDir = sh(script: 'pwd', returnStdout: true).trim()
                    } else {
                        workspaceDir = bat(script: 'echo %WORKSPACE%', returnStatus: true).trim()
                    }						
				    //def workspaceDir = pwd()
                    
                    // Run the .NET Core build and publish commands
                    bat "cd ${workspaceDir}"
                    //bat "${DOTNET_ROOT}\\dotnet publish -c Release -o ./publish"
					  //bat 
			bat "${PATH_TO_DOTNET_SDK}/dotnet publish -c Release -o ./publish"

					
					 // Copy the published files to the shared folder
                    //def sharedFolderPath = "C:\\path\\to\\shared\\folder" // Update with your shared folder path
					def sharedFolderPath = "C:\\sharedf"
                    bat "xcopy /E /I /Y ${workspaceDir}\\publish ${sharedFolderPath}"
                }
            }
        }
    }
    
    post {
        success {
            archiveArtifacts artifacts: '**/publish/**', allowEmptyArchive: true
        }
    }
}