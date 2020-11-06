node{
  stage('SCM Checkout'){
    git 'https://github.com/ashish456747/demo.git'
  }
  stage('Compile Package'){
    //Get maven home path
    def mvnHome=tool name: 'maven', type: 'maven'
    sh "${mvnHome}/bin/mvn package"
  }
  stage('Email Notification'){
    mail bcc: '', body: 'test', cc: '', from: '', replyTo: '', subject: 'pipeline02 email notification', to: 'ashish.v.kumar7@gmail.com'  
  }
}
