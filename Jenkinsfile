pipeline{
	agent any
	environment{
		scannerHome=tool name: 'scanner-dotnet-home', type: 'hudson.plugins.scanner.MsBuildSQRunnerInstallation'
		dtr="nishugoel0411"
	}
	stages{
		stage('checkout'){
			steps{
				checkout scm
			}
		}
		stage('nuget'){
			steps{
				bat "dotnet restore"
			}
		}
	}
}