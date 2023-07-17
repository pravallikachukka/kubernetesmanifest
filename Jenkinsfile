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
            steps {           
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'GIT_ID', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                            sh "git config user.email pravallika@gmail.com"
                            sh "git config user.name pravallikachukka"
                            //sh "git switch master"                            
                            sh "cat deployment.yaml"
                            sh "sed -i 's+chukkap/kubernetesproject.*+chukkap/kubernetesproject:${DOCKERTAG}+g' deployment.yaml"
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
                        }
                    }
                }
            }
        }

    }
}
