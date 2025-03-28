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
                        sh "git config user.email aek.mabrouk@gmail.com"
                        sh "git config user.name akmabrouk"
                        //sh "git switch master"
                        sh "cat deployment-service.yaml"
                        sh "sed -i 's+akmabrdockerid/test.*+akmabrdockerid/test:${DOCKERTAG}+g' deployment-service.yaml"
                        sh "cat deployment-service.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/jenkins-argocd-manifest.git HEAD:main"
      }
    }
  }
}
}
