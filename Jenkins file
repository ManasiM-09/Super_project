pipeline {
    agent any
    environment {
  Buck_name = "my-latest-buck"
}


    stages {
        stage('Git clone') {
            steps {
                echo 'Clonned code from github'
                git branch: 'main', url: 'https://github.com/ManasiM-09/Jenkins_practice.git'
            }
        }
        stage('conditional statements') {
            steps {
                echo 'if else statement'
                sh '''
                if  aws s3 ls s3://${Buck_name};then
                    echo "Bucket already exists" 
                else 
                    aws s3 mb s3://${Buck_name}
                    echo "Bucket created sucessfully"
                fi
                  '''
                  }
             }
        stage('deploy on both'){
            parallel{
                stage('Deploy to both'){
                    steps {
                        echo 'Deploying bucket to s3'
                        sh 'aws s3 sync . s3://${Buck_name}'
             }
         }
         stage('Deploy to Ec2') {
                    steps {
                        echo 'Deploying to Ec2'
                        sh 'sudo rm -rf /var/www/html/*'
                        sh 'sudo cp -r . /var/www/html'
              }
            }
         }
      }
   }
}
