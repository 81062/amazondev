node{
    
    stage('Clone repo'){
        git branch: 'main', credentialsId: 'a3dcf376-7386-46b6-9bba-0dc90a61247f', url: 'https://github.com/81062/amazondev.git'
    }
    stage('Maven Build'){
        def mavenHome = tool name: "Maven-3.8.7", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
   }
    
}   
   
   