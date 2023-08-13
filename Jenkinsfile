pipeline {
    agent none
    stages {
        stage('Test') {
            agent {
                docker {
                    image 'bitnami/pytorch:latest'
                    args '-u 1001:0'
                }
           }
           
           steps {
                sh 'pip3 install flask parameterized'
                sh '''
                    cd train
                    python3 -m unittest train_test.py
                '''
                sh '''
                    cd infer
                    python3 infer_test.py
                '''
           }
        }
    }

    post {
        // 유닛 테스트가 실패
        failure {
            echo "Fail"
        }
        success {
            echo "Success"
        }
    }
}