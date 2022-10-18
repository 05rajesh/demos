pipeline {
    agent any
    stages {
        stage("Build") {
            step {
                sh 'printenv'
            }
        }
        stage("Publich ECR") {
            steps {
                withEnv(["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRETS_ACCESS_KEY=${env.AWS_SECRETS_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) 
                {
                    sh 'docker login -u AWS -p (aws ecr get-login-password --region ap-south-1) 877131812078.dkr.ecr.ap-south-1.amazonaws.com'
                    sh 'docker build -t ecrRajeshDemo .'
                    sh 'docker tag ecrRajeshDemo:"$BUILD_ID" 877131812078.dkr.ecr.ap-south-1.amazonaws.com/ecrRajeshDemo:"$BUILD_ID"'
                    sh 'docker push 877131812078.dkr.ecr.ap-south-1.amazonaws.com/ecrRajeshDemo:"$BUILD_ID"'
                }
            }
        }
    }
}