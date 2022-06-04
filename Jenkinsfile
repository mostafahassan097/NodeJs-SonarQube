pipeline {
    agent {label "ubuntu_slave"}

   stages {
      stage('CLONE') {
         steps {
               git credentialsId: 'gitcreds', url: 'https://github.com/mostafahassan097/autom8able-mochajs-starter.git'
         }
      }

      stage('SonarQube Analysis') {
          
            environment {

                scannerHome = tool 'sonar-scanner'

            }


         steps {
             nodejs(nodeJSInstallationName: 'nodejs'){
                 sh 'npm install'

                 withSonarQubeEnv('sonar-server')
                 {
                    sh 'npm install --save-dev mocha chai'
                    sh "npm audit fix"
                    sh 'npm run test'
                    sh " ${scannerHome}/bin/sonar-scanner "
                 }
             }
         }
      }
    }
   
}