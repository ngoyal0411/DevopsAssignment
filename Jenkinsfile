pipeline{
	agent any
	environment{
		branch="Develop"
		scannerHome= tool name: 'sonar_scanner_dotnet', type: 'hudson.plugins.sonar.MsBuildSQRunnerInstallation'
		dtr="nishugoel0411"
	}
	stages{
		stage('checkout'){
			steps{
				checkout([$class: 'GitSCM', branches: [[name: '*/${branch}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '6f0eb1a7-201a-4036-a46a-ca2544b43a11', url: 'url: \'https://github.com/ngoyal0411/DevopsAssignment.git\'']]])
			}
		}
		stage('nuget'){
			steps{
				bat "dotnet restore"
			}
		}
		stage('Start SonarQube Analysis'){
			steps{
				withSonarQubeEnv('Test_Sonar'){
					bat "dotnet ${scannerHome}/SonarScanner.MSBuild.dll begin /k:nagp-hello-world /n:nagp-hello-world /v:1.0"
				}
			}
		}
		stage('build'){
			steps{
				bat "dotnet build -c Release -o WebApplication4/app/build"
			}
		}
		stage('SonarQube Analysis End'){
			steps{
				withSonarQubeEnv('Test_Sonar'){
					bat "dotnet ${scannerHome}/SonarScanner.MSBuild.dll end"
				}
			}
		}
		stage('Release Artifacts'){
			steps{
				bat "dotnet publish -c Release -o WebApplication4/app/publish"
			}
		}
		stage('Build Docker File'){
			steps{
				bat "docker build --no-cache -t ${dtr}/webapp4v1:${BUILD_NUMBER} ."
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