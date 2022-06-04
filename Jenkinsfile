pipeline {
    agent {label "ubuntu_slave"}

   stages {
      stage('SonarQube Analysis') {
          
            environment {

                scannerHome = tool 'sonar-scanner'

            }


         steps {
             nodejs(nodeJSInstallationName: 'nodejs'){

                def repositoryUrl = scm.userRemoteConfigs[0].getUrl()
                def GIT_REPO_NAME = scm.userRemoteConfigs[0].getUrl().tokenize('/').last().split("\\.")[0]

                 sh 'npm install'

                 withSonarQubeEnv('sonar-server')
                 {
                    sh 'npm install --save-dev mocha chai'
                    sh "npm audit fix"
                    sh 'npm run test'
                    sh "sed -i s#{{repo_name}}#${GIT_REPO_NAME}# sonar-project.properties"
                    sh "sed -i s#{{branch_name}}#${SONAR_BRANCH_NAME}# sonar-project.properties"
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectVersion=${SONAR_BRANCH_NAME} -Dsonar.buildString=Jenkins-${SONAR_BRANCH_NAME}-BLD${env.BUILD_NUMBER}"
                 }
             }
         }
      }
    }
   
}