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
                        sh 'docker build -t gcr.io/eternal-psyche-256708/1.0-${BUILD_NUMBER} .'
                        sh 'docker push gcr.io/eternal-psyche-256708/1.0-${BUILD_NUMBER}'
                    }
                }
                stage("Build Dev") {
                    when {
                        branch 'dev'
                    }
                    steps{
                        echo "========executing Dev Build========"
                        sh 'docker build -t gcr.io/eternal-psyche-256708/dev-${GIT_COMMIT} .'
                        sh 'docker push gcr.io/eternal-psyche-256708/1.0-${GIT_COMMIT}'
                    }
                }
                stage("Build Staging") {
                    when {
                        branch 'staging'
                    }
                    steps{
                        echo "========executing Staging Build========"
                        sh 'docker build -t gcr.io/eternal-psyche-256708/staging-${GIT_COMMIT} .'
                        sh 'docker push gcr.io/eternal-psyche-256708/staging-${GIT_COMMIT}'
                    }
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}