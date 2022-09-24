pipeline {
  agent any
  stages {
    stage('install test tools') {
      steps {
        sh 'pip3 install nose coverage nosexcover pylint'
      }
    }

    stage('nose tests') {
      steps {
        sh '''nosetests -sv --with-xunit --xunit-file=nosetests.xml --with-xcoverage --xcoverage-file=coverage.xml
'''
      }
    }

    stage('sonar scanner') {
      steps {
        withSonarQubeEnv(installationName: 'SonarQube', credentialsId: 'sonar', envOnly: true) {
          waitForQualityGate(credentialsId: 'sonar', webhookSecretId: 'sonar')
        }

      }
    }

  }
}