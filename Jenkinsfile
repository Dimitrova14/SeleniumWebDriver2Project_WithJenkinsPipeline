pipeline {
    agent any

    stages {
        stage('Checkout repository') {
            //checkout repository
            steps {
                git branch: 'main', url: 'https://github.com/Dimitrova14/SeleniumWebDriver2Project_WithJenkinsPipeline'
            }
            
        }
        stage('Setup .NET environment') {
            //setup .net environment
            steps {
                bat '''
                echo Installing .NET 6 SDK
                curl -l -o dotnet-sdk-6.0.132-win-x64.exe https://download.visualstudio.microsoft.com/download/pr/0c82e7e6-fdde-49f2-a69f-bd986aeafe1b/9ea7411a22e661fff0e61e56a466e484/dotnet-sdk-6.0.132-win-x64.exe 
                dotnet-sdk-6.0.132-win-x64.exe /quiet /norestart
                '''
            }
            
        }
        stage('Restore dependencies') {
            //install dependencies
            steps {
                bat 'dotnet restore SeleniumBasicExercise.sln'
            }
            
        }
        stage('Build') {
            //build
            steps {
                bat 'dotnet build SeleniumBasicExercise.sln --configuration Release'
            }
            
        }
        stage('Run tests TestProject1') {
            //run tests
            steps {
                bat 'dotnet test TestProject1/TestProject1.csproj --logger "trx;LogFileName=TestResults.trx'
            }
            
        }
        stage('Run tests TestProject2') {
            //run tests
            steps {
                bat 'dotnet test TestProject2/TestProject2.csproj --logger "trx;LogFileName=TestResults.trx'
            }
            
        }
        stage('Run tests TestProject3') {
            //run tests
            steps {
                bat 'dotnet test TestProject3/TestProject3.csproj --logger "trx;LogFileName=TestResults.trx'
            }
            
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step ([

                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'

            ])
        }
    }
}