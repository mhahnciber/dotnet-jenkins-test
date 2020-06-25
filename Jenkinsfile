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
        dotnet pack --no-build --output nupkgs --version-suffix=${BUILD_ID}
	dir nupkgs
        dotnet nuget push --skip-duplicate -s http://localhost:5000/v3/index.json nupkgs\lib-test.1.0.0-${BUILD_ID}.nupkg
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
        dotnet pack --no-build --output nupkgs
	dir nupkgs
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
        echo web api projects are generally not packed with nuget
	
    """
   }
  }

 }
}