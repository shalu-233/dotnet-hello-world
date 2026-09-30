pipeline {
    agent { label 'dotnet' }
    options {
        timeout ( time: 1, unit: 'HOURS' )
    }
    parameters {
        string( name: 'branch', defaultValue : 'main')
        string( name: 'giturl', defaultValue: 'https://github.com/dotnet/samples.git' )
        string( name: 'BUILDPATH', defaultValue: 'hello-world-api/hello-world-api.csproj')
        string( name: 'directory', defaultValue: 'published')
    }
    stages {
        stage ('scm') {
            steps {
                git branch: "$(params.branch)",
                    url: "$(giturl)"
            }
        }
        stage ('build') {
            steps {
                sh "dotnet build -c Release $(BUILDPATH)",
                sh "mkdir $(directory) && dotnet publish -o ./$(directory) -c Release $(BUILDPATH)"
            }
        }
        post {
            success {
                echo "this is completed"
            }
        }
    }
}