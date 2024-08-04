pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the repository
                git branch: 'main', url: 'https://github.com/xchshark/Jenkins_Selenium'
            }
        }

        stage('Dependencies') {
            steps {
                // Restore dependencies
                bat 'dotnet restore SeleniumIde.sln'
            }
        }

        stage('Build') {
            steps {
                // Build the project
                bat 'dotnet build SeleniumIde.sln --configuration Release'
            }
        }

        stage('Tests') {
            steps {
                // Run tests
                bat 'dotnet test SeleniumIde.sln --logger trx;LogFileName=TestResults.trx'
            }
        }
    }

    post {
        always {
            // Archive test results and publish MSTest results
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'
            ])
        }
    }
}
