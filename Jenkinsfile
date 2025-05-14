pipeline {
  agent any

  environment {
    AWS_REGION = 'us-east-1'
    STACK_NAME = 'MyVPCStack'
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/raju0509/demo23.git'
      }
    }

    stage('Validate CF Template') {
      steps {
        sh 'aws cloudformation validate-template --template-body file://jaimax-devops.yaml'
      }
    }

    stage('Deploy Stack') {
      steps {
        sh '''
          aws cloudformation deploy \
            --template-file jaimax-devops.yml \
            --stack-name ${STACK_NAME} \
            --capabilities CAPABILITY_NAMED_IAM \
            --region ${AWS_REGION}
        '''
      }
    }
  }
}
