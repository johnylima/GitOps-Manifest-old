node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email johny.limasp@gmail.com"
                        sh "git config user.name Johny Lima"
                        //sh "git switch master"
                        sh "cat phone-validator-backend-deployment.yaml"
                        sh "sed -i 's+johnylima/phone-validator-backend.*+johnylima/phone-validator-backend:${DOCKERTAG}+g' phone-validator-backend-deployment.yaml"
                        sh "cat phone-validator-backend-deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/GitOps-Manifest-2.git HEAD:gitops/phone-validator-backend"
      }
    }
  }
}
}