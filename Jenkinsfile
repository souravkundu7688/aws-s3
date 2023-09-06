pipeline{
    agent any
    triggers {
	pollSCM '* * * * *'
    }
    stages{
	stage('build'){
		steps{
			build job: "test-build", propagate: true, wait: true
		}
	}
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
      						pwd
						sh aws_ec2_verify.sh
						'''
                    }
            }
        }
    }
}
