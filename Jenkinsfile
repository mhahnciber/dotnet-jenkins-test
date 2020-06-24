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

  stage('build lib') {
   steps {
    bat """
        cd lib-test
        dotnet restore
        dotnet clean
        dotnet build --configuration Debug
        dotnet nuget pack --no-build --output nupkgs
	dir 
    """
   }
  }
  
  stage('build cmd') {
   steps {
    bat """
        cd cmd-test
        dotnet restore
        dotnet clean
        dotnet build --configuration Debug
        dotnet nuget pack --no-build --output nupkgs
	dir 
    """
   }
  }
  
  stage('build api') {
   steps {
    bat """
        cd api-test
        dotnet restore
        dotnet clean
        dotnet build --configuration Debug
        dotnet nuget pack --no-build --output nupkgs
	dir 
    """
   }
  }

 }
}