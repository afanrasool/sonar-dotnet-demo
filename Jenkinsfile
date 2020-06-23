pipeline {
  agent none
  stages {
    stage('Scan Codebase') {
      agent { label 'sonar-dotnet' }
      steps {
        withSonarQubeEnv('SonarQube-Server') {
          sh "dotnet sonarscanner begin /k:peopleapi /k:sonarqube_project_key=peopleapi /d:sonar.scm.exclusions.disabled=true /d:sonar.scm.enabled=true /d:sonar.scm.provider=git /d:sonar.host.url=$SONAR_HOST_URL /d:sonar.login=$SONAR_AUTH_TOKEN"
          sh "dotnet build"
          sh "dotnet sonarscanner end /d:sonar.login=$SONAR_AUTH_TOKEN"
        }
      }
    }
    /*  You may need a docker-in-docker to run this on a Jenkins slave agent and do not like doing that */
    /*
    stage('Microscanner security scan'){
      steps {
        aquaMicroscanner imageName: 'peopleapi/peopleapi:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html'
      }
    }
    */
  }
}
