pipeline{
    agent any
    stages{
        stage("Build"){
            stages {
                stage("Build Master") {
                    when {
                        branch 'master'
                    }
                    steps{
                        echo "========executing Master Build========"
                        sh 'docker build -t shukiyahu/echo_ex:1.0.${BUILD_NUMBER} .'
                        sh 'docker push shukiyahu/echo_ex:1.0.${BUILD_NUMBER}'
                    }
                }
                stage("Build Dev") {
                    when {
                        branch 'dev'
                    }
                    steps{
                        echo "========executing Dev Build========"
                        sh 'docker build -t shukiyahu/echo_ex:dev-${GIT_COMMIT} .'
                        sh 'docker push shukiyahu/echo_ex:dev-${GIT_COMMIT}'
                    }
                }
                stage("Build Staging") {
                    when {
                        branch 'staging'
                    }
                    steps{
                        echo "========executing Staging Build========"
                        sh 'docker build -t shukiyahu/echo_ex:staging-${GIT_COMMIT} .'
                        sh 'docker push shukiyahu/echo_ex:staging-${GIT_COMMIT}'
                    }
                }
            }
        }
    }
}