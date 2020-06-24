pipeline {
 agent any
 environment {
  dotnet = 'dotnet.exe'
 }
 stages {
  stage('System Information for Debugging') {
   steps {
    bat "where git"
    bat "set"
    bat "dir"
   }
  }

  stage('Restore PACKAGES') {
   steps {
    bat "cd lib-test"
    bat "dotnet restore"
   }
  }
  stage('Clean') {
   steps {
    bat "cd lib-test"
    bat 'dotnet clean'
   }
  }
  stage('Build') {
   steps {
    bat "cd lib-test"
    bat 'dotnet build --configuration Release'
   }
  }
  stage('Pack') {
   steps {
    bat 'dotnet pack --no-build --output nupkgs'
   }
  }
  stage('Publish') {
   steps {
    bat "dotnet nuget push **\\nupkgs\\*.nupkg -k yourApiKey -s   http://myserver/artifactory/api/nuget/nuget-internal-stable/com/sample"
   }
  }
 }
}