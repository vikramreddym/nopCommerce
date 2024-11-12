pipeline {
    agent { label 'DOTNET' }
    // triggers {
    //     pollSCM('* * * * 1-5')
    // }
    stages {
        stage('git-clone') {
            steps {
                git branch: 'master', url: 'https://github.com/vikramreddym/nopCommerce.git'
            }
        }
        stage('Build the code') {
            steps {
                sh 'dotnet build -c Release src/NopCommerce.sln'
                sh 'dotnet publish -c Release src/Presentation/Nop.Web/Nop.Web.csproj -o "./published"'
            }
            post {
                success {
                    sh 'mkdir ./published/bin ./published/logs'
                    sh 'tar -czvf nop.web.tar.gz ./published/'
                    archiveArtifacts artifacts: '**/*.tar.gz'
                }
            }
        }
    }
}