pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages {
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
                sh "rm -rf tools"
                sh "dotnet tool install dotnet-reportgenerator-globaltool --tool-path tools"
                // sh "ls -R"
                sh "./tools/reportgenerator -reports:**/coverage.cobertura.xml -targetdir:BuildReports/Coverage -reporttypes:'HTML;HTMLSummary'"
            }
        }
        stage("Code Coverage Report") {
            steps {
                // sh "ls"
                // sh "ls -R ./BuildReports"
                publishHTML (target : [ reportDir: './BuildReports/Coverage', reportFiles: 'index.html', reportName: 'Code Coverage Report'])
            }
        }
    }
}