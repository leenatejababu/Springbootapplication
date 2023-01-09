node {

def IMAGE_NAME = params.IMAGE_NAME
def TAG_NAME = params.TAG_NAME
 def TAG_NAME_Latest = params.TAG_NAME_Latest
 def Jfog_Ip = params.Jfog_Ip
 def Jfog_Port = params.Jfog_Port
 def Repository_Key = params.Repository_Key
 
// def docker_login = params.docker_login
// def Dockerhub_URL = params.Dockerhub_URL

stage('Checkout') {
  git branch: 'main', credentialsId: 'Leena-Git', url: 'https://github.com/leenatejababu/Springbootapplication.git'  
 }


stage('Build') {
    withMaven(jdk: 'JAVA', maven: 'maven') {
        
        println "build is running"
        sh 'mvn clean package'
    }
}


stage('Build Image'){
    sh  """ 
        docker version
        docker build -t springboot:1.0.0 .
        docker tag springboot:1.0.0 leenatejababu/springboot:1.0.0
        docker login -u leenatejababu -p ltb@11041986 
        docker push leenatejababu/springboot:1.0.0  
       """
}
 
 stage('deploy to kubernetes'){
withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'KUBEconfig', namespace: '', serverUrl: '') {

    sh """
     kubectl cluster-info
     kubectl get po
     """
 }
 }
}
