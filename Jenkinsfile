node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github-PAT', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh """
                        git config user.email singhajeet24@outlook.com
                        git config user.name Ajeet
                        cat deployment.yaml
                        sed -i 's+as35/test.*+as35/test:${DOCKERTAG}+g' deployment.yaml
                        cat deployment.yaml
                        git add .
                        git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'

                        # Construct the Git URL
                        GIT_URL="https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/jenkins-argocd-pipeline-deploy.git"

                        # Debug the constructed URL
                        echo \$GIT_URL

                        # Use the constructed URL
                        git push \$GIT_URL HEAD:main
                    """
                }
            }
        }
    }
}
