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
		stage('build'){
			steps{
				bat "dotnet build -c Release -o WebApplication4/app/build"
			}
		}
		stage('Release Artifacts'){
			steps{
				bat "dotnet publish -c Release -o WebApplication4/app/publish"
			}
		}
	}
}