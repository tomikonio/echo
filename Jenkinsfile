pipeline{
    agent any
    post {
        failure {
            updateGitlabCommitStatus name: 'Build', state: 'failed'
            updateGitlabCommitStatus name: 'Publish', state: 'failed'
        }
        success {
            updateGitlabCommitStatus name: 'Build', state: 'success'
            updateGitlabCommitStatus name: 'Publish', state: 'success'
        }
    }
    options
    {
        gitLabConnection('Gitlab')
        gitlabBuilds(builds: ['Build', 'Publish'])
    }
    triggers
    {
        gitlab(
        triggerOnPush: true,
        triggerOnMergeRequest: true,
        branchFilterType: 'All',
        addVoteOnMergeRequest: true)
    }
    stages{
        stage("Build"){
            steps {
                script {
                    if ("$GIT_BRANCH" == 'master') {
                        sh('docker build -t shukiyahu/echo_ex:1.0.${BUILD_NUMBER} .')
                    }
                    else if ("$GIT_BRANCH" == 'dev') {
                        sh('docker build -t shukiyahu/echo_ex:dev-${GIT_COMMIT} .')
                    }
                    else if ("$GIT_BRANCH" == 'staging') {
                        sh('docker build -t shukiyahu/echo_ex:staging-${GIT_COMMIT} .')
                    }
                }
            }
        }
        stage("Publish") {
            steps {
                script {
                    if ("$GIT_BRANCH" == 'master') {
                        sh('docker push shukiyahu/echo_ex:1.0.${BUILD_NUMBER}')
                    }
                    else if ("$GIT_BRANCH" == 'dev') {
                        sh('docker push shukiyahu/echo_ex:dev-${GIT_COMMIT}')
                    }
                    else if ("$GIT_BRANCH" == 'staging') {
                        sh('docker push shukiyahu/echo_ex:staging-${GIT_COMMIT}')
                    }
                }
            }
        }
    }
}