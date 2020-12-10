node{
  stage('SCM Checkout'){
    git 'https://github.com/ashish456747/demo.git'
  }
  stage('Compile Package'){
    //Get maven home path
    def mvnHome=tool name: 'maven', type: 'maven'
    sh "${mvnHome}/bin/mvn clean package"
  }
  stage('Upload Artifact to nexus'){
    nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', file: 'target/myweb-1.0.0.war', type: 'war']], credentialsId: 'nexus3', groupId: 'in.javahome', nexusUrl: '192.168.1.14', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://192.168.1.14:8081/repository/simpleapp-release/', version: '1.0.0'
  }
  stage('SonarQube Analysis'){
    def mvnHome=tool name:'maven', type:'maven'
    withSonarQubeEnv('sonar-6'){
      sh "${mvnHome}/bin/mvn sonar:sonar"
    }
  }
  stage("Quality Gate"){
    timeout(time: 1, unit: 'HOURS') {
      def qg = waitForQualityGate()
      if (qg.status != 'OK') {
        slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#test', color: 'danger', message: 'SonarQube Analysis failed', teamDomain: 'AppDev', tokenCredentialId: 'slack-demo'
        error "Pipeline aborted due to quality gate failure: ${qg.status}"
      }
    }
  }
  stage('Email Notification'){
    mail bcc: '', body: 'test', cc: '', from: '', replyTo: '', subject: 'pipeline02 email notification', to: 'ashish.v.kumar7@gmail.com'  
  }
  stage('Slack Notification'){
    slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#test', color: 'good', message: 'Welcome to Jenkins!', teamDomain: 'AppDev', tokenCredentialId: 'slack-demo'
  }
}
