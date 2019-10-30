pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                echo "========executing Build========"
                sh 'docker build -t gcr.io/eternal-psyche-256708/1.0-${BUILD_NUMBER}'
                sh 'docker push gcr.io/eternal-psyche-256708/1.0-${BUILD_NUMBER}'
            }
            // post{
            //     always{
            //         echo "========always========"
            //     }
            //     success{
            //         echo "========A executed successfully========"
            //     }
            //     failure{
            //         echo "========A execution failed========"
            //     }
            // }
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