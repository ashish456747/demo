node{
  stage('SCM Checkout'){
    git 'https://github.com/ashish456747/demo.git'
  }
  stage('Compile Package'){
    //Get maven home path
    def mvnHome=tool name: 'maven', type: 'maven'
    sh "${mvnHome}/bin/mvn package"
  }
}
