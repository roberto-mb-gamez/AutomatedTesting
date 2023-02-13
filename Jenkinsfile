pipeline {
    agent any
    stages {
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
                sh "dotnet test -f net5.0"
            }
        }
    }
}