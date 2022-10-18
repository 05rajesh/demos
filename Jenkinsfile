pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                sh 'printenv'
            }
        }
        stage("Publich ECR") {
            steps {
                withEnv (["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRETS_ACCESS_KEY=${env.AWS_SECRETS_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) 
                {
                    sh 'docker login -u AWS --password-stdin $(aws ecr get-login-password --region ap-south-1) public.ecr.aws/o2h9c4i8'
                    sh 'docker build -t demo .'
                    sh 'docker tag demo:latest public.ecr.aws/o2h9c4i8/demo:"$BUILD_ID"'
                    sh 'docker push public.ecr.aws/o2h9c4i8/demo:"$BUILD_ID"'
                }
            }
        }
    }
}