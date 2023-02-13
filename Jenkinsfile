pipeline {
    agent any
    stages {
        stage("Install tools") {
            steps {
                sh "if [ -d 'tools']; then rm -d tools ; fi"
                sh "dotnet tool install dotnet-reportgenerator-globaltool --tool-path tools"
            }
        }
        stage("Compile") {
            steps {
                sh "dotnet build"
            }
        }
        stage("Tests") {
            steps {
                sh "dotnet test -f net5.0 --logger 'trx;LogFileName=TestResults.trx' --logger 'xunit;LogFileName=TestResults.xml' --results-directory ./BuildReports/TestResults /p:CollectCoverage=true /p:CoverletOutput=BuildReports/Coverage/ /p:CoverletOutputFormat=cobertura /p:Exclude='[xunit.*]*'"
            }
        }
        stage("Code coverage") {
            steps {
                sh "dotnet-reportgenerator-globaltool -reports:**/coverage.cobertura.xml -targetdir:BuildReports/Coverage -reporttypes:'HTML;HTMLSummary'"
            }
        }
    }
}