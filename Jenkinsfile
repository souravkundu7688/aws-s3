pipeline{
    agent any
    stages{
        stage('verify'){
            steps{
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){
                        sh '''
						cd aws_file
						sh aws_s3_verfiy.sh
						hostname -i
						'''
                    }
            }
        }
    }
}
