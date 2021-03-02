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
		stage('Build Docker File'){
			steps{
				bat "docker build --no-cache -t ${dtr}/webapp4v1:${BUILD_NUMBER}"
			}
		}
		stage('Push Image to docker hub'){
			steps{
				bat "docker push ${dtr}/webapp4v1:${BUILD_NUMBER}"
			}
		}
		stage('Docker Deployment'){
			steps{
				bat "docker run --name c-mydevopscontainer -d -p 6001:80 ${dtr}/webapp4v1:${BUILD_NUMBER}"
			}
		}
	}
}