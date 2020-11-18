node{
  stage('SCM Checkout'){
    git 'https://github.com/ashish456747/demo.git'
  }
  stage('Compile Package'){
    //Get maven home path
    def mvnHome=tool name: 'maven', type: 'maven'
    sh "${mvnHome}/bin/mvn package"
  }
  stage('SonarQube Analysis'){
    def mvnname=tool name:'maven', type:'maven',
      withSonarQubeEnv('sonar-6'){
        sh "${mvnname}/bin/mvn sonar:sonar"
      }
  }
  stage('Email Notification'){
    mail bcc: '', body: 'test', cc: '', from: '', replyTo: '', subject: 'pipeline02 email notification', to: 'ashish.v.kumar7@gmail.com'  
  }
  stage('Slack Notification'){
    slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#test', color: 'good', message: 'Welcome to Jenkins!', teamDomain: 'AppDev', tokenCredentialId: 'slack-demo'
  }
}
