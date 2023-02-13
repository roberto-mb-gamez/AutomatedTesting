pipeline {
    agent any
    stages {
        stage("Prepare") {
            steps {
                // Clean Jenkins workspace.
                cleanWs()
            }

        }
        stage("SDK Versions") {
            steps {
                sh "dotnet --list-sdks"
            }
        }
        stage("Compile") {
            steps {
                sh "dotnet build"
            }
        }
         stage("Unit Test") {
            steps {
                // sh "dotnet tool install dotnet-reportgenerator-globaltool --tool-path tools"
                sh "dotnet test -f net5.0 --logger 'trx;LogFileName=TestResults.trx' --logger 'xunit;LogFileName=TestResults.xml' --results-directory ./BuildReports/UnitTests /p:CollectCoverage=true /p:CoverletOutput=BuildReports/Coverage/ /p:CoverletOutputFormat=cobertura /p:Exclude='[xunit.*]*'"
            }
        }
    }
}