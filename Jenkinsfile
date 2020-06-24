pipeline {
 agent any
 environment {
  dotnet = 'dotnet.exe'
 }
 stages {
  stage('Checkout') {
   steps {
    git credentialsId: 'userId', url: 'https://github.com/NeelBhatt/SampleCliApp', branch: 'master'
   }
  }
  stage('System Information for Debugging') {
   steps {
    bat "where git"
    bat "dir"
    bat "set"
   }
  }

  stage('Restore PACKAGES') {
   steps {
    bat "dotnet restore --configfile NuGet.Config"
   }
  }
  stage('Clean') {
   steps {
    bat 'dotnet clean'
   }
  }
  stage('Build') {
   steps {
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