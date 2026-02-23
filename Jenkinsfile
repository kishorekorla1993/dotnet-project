pipeline {
    agent any

    stages {
        stage('Check .NET') {
            steps {
                sh 'dotnet --version'
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --configuration Release'
            }
        }

        stage('Publish') {
            steps {
                sh 'dotnet publish -c Release -o publish'
            }
        }

        stage('Package (tar)') {
            steps {
                sh '''
                mkdir -p dist
                tar -czvf dist/dotnet-sample.tar.gz publish
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'dist/*.tar.gz', fingerprint: true
        }
    }
}
