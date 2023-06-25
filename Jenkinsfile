pipeline {
    agent any   

    stages {
        stage('checkout') {
            steps {
                script{
                    echo 'cloning stage'
                    git branch: 'main', url: 'https://github.com/pravallikachukka/kubernetesmanifest.git'
                }                
            }
        }
        stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email pravallika@gmail.com"
                        sh "git config user.name pravallika"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sh "sed -i 's+chukkap/flaskap.*+chukkap/flaskap:${DOCKERTAG}+g' deployment.yaml""
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://github.com/pravallikachukka/kubernetesmanifest.git HEAD:main"
                    }
                }
            }
        }

    }
}
