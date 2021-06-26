pipeline {

    agent any
        environment {
       LT_BUILD_NAME = "test-LT-pipeline"
    }
    stages{

      stage('Setup') {
        steps {
            cleanWs()
            sh 'wget https://downloads.lambdatest.com/tunnel/v3/linux/64bit/LT_Linux.zip'
            //sh 'sudo apt-get install zip unzip'
            sh 'unzip -o LT_Linux.zip'
            sh "./LT  --user ${LT_USERNAME} --key ${LT_ACCESS_KEY} --tunnelName jenkins-tunnel &"
        }
      }
      stage('Test') {
        steps {
            sh 'sleep 10'
            sh 'python3 -m http.server 8081 &'
            sh 'python3 sample-todo-app/test_sample_todo_app.py'
            sh 'pkill -f "http.server"'
            sh 'sleep 30'
            sh 'pkill -f "jenkins-tunnel"'
        }
      }
    }

}
