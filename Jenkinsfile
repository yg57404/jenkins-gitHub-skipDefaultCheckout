pipeline {
  agent {label 'linux1'}
  
 options {
        skipDefaultCheckout true
    }   
  
        
  stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        }
        stage('Deploy') {
          steps{
        sh 'yum install git -y'
        sh 'sudo yum install nginx -y'
        sh 'cd /etc/nginx; sudo service nginx start' 
        sh 'cd /root/; sudo yum install python-pip -y'
        sh 'sudo yum install python-virtualenv -y'
        sh 'mkdir /root/yogesh'
        sh 'cd /root/yogesh/; [ -d "/root/yogesh/op" ] && sudo git pull || sudo git clone git@github.com:yg57404/op.git'
        sh 'cd /root/yogesh/; virtualenv venv ;source /root/yogesh/venv/bin/activate ; pip install -r /root/yogesh/op/requirements.txt ; ' 
        sh 'cd /root/yogesh/op; gunicorn --bind 0.0.0.0:9090 restapi.wsgi &'
     }
   }
 }
}
