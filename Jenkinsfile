pipeline {
    agent any
    parameters {
        string(defaultValue: '', description: 'Enter Environment Name (Available Environments: dev & prod) :', name: 'environment', trim: false)
        string(defaultValue: 'latest', description: 'Enter BUILD NUMBER to deploy [Default Value: latest]:', name: 'input', trim: false)
    }
 stages {
     stage('Pull file from S3 ') {
            steps {
                sh 'aws s3 cp s3://kupos-at-project/${input}.zip .'
            }
        }      
     stage("Deploy"){
           steps{
                script {
                    if ( params.environment=='prod') {
                        sh 'cp ${input}.zip /home/ec2-user/prod_environment'
                        sh 'unzip ${input}.zip'
                        sh 'rm ${input}.zip'
                    } else if ( params.environment=='dev') {
                        sh 'cp ${input}.zip /home/ec2-user/dev_environment'
                        sh 'unzip ${input}.zip'
                        sh 'rm ${input}.zip'
                    }
                 }              
              } 
          }
     }
}
