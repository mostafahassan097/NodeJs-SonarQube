pipeline {
    agent {label "ubuntu_slave"}

   stages {
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