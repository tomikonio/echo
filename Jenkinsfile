pipeline{
    agent any
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
                        sh('docker push shukiyahu/echo_ex:dev-${GIT_COMMIT} .')
                    }
                    else if ("$GIT_BRANCH" == 'staging') {
                        sh('docker push shukiyahu/echo_ex:staging-${GIT_COMMIT} .')
                    }
                }
            }
        }
        // stages {
        //     stage("Build Master") {
        //         when {
        //             branch 'master'
        //         }
        //         steps{
        //             echo "========executing Master Build========"
        //             sh 'docker build -t shukiyahu/echo_ex:1.0.${BUILD_NUMBER} .'
        //             sh 'docker push shukiyahu/echo_ex:1.0.${BUILD_NUMBER}'
        //         }
        //     }
        //     stage("Build Dev") {
        //         when {
        //             branch 'dev'
        //         }
        //         steps{
        //             echo "========executing Dev Build========"
        //             sh 'docker build -t shukiyahu/echo_ex:dev-${GIT_COMMIT} .'
        //             sh 'docker push shukiyahu/echo_ex:dev-${GIT_COMMIT}'
        //         }
        //     }
        //     stage("Build Staging") {
        //         when {
        //             branch 'staging'
        //         }
        //         steps{
        //             echo "========executing Staging Build========"
        //             sh 'docker build -t shukiyahu/echo_ex:staging-${GIT_COMMIT} .'
        //             sh 'docker push shukiyahu/echo_ex:staging-${GIT_COMMIT}'
        //         }
        //     }
    }
}