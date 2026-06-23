pipeline {
     // 전역 에이전트를 사용하지 않음으로써 컨테이너 중첩 방지
    agent none

    environment {
        AWS_DEFAULT_REGION = 'ap-northeast-2'
    }

    stages {

        stage('Deploy to AWS') {
            agent {
                docker {
                    image 'amazon/aws-cli'
                    reuseNode true
                    args "--entrypoint=''"
                }
            }

            environment {
                AWS_S3_BUCKET = 'learn-jenkins-20260621'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'my-aws', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    sh '''
                        aws --version
                        aws ecs register-task-definition \
                            --cli-input-json file://aws/task-definition-prod.json/sleep360.json
                    '''
                }
            }
        }

    }


}
