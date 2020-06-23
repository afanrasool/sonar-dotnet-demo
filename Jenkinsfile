pipeline {
  agent none
  stages {
    stage('Scan Codebase') {
      agent { label 'sonar-dotnet-agent' }
      steps {
        withSonarQubeEnv('SonarQube-Server') {
          sh "dotnet /sonar-scanner/SonarScanner.MSBuild.dll begin /k:peopleapi /d:sonar.host.url=$SONAR_HOST_URL /d:sonar.login=$SONAR_AUTH_TOKEN"
          sh "dotnet build"
          sh "dotnet /sonar-scanner/SonarScanner.MSBuild.dll end /d:sonar.login=$SONAR_AUTH_TOKEN"
        }
      }
    }
  }
}
