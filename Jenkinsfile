pipeline{
	agent any
	environment{
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