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
  git credentialsId:'Github-Login', url: 'https://github.com/leenatejababu/ADOK8'  
 }


stage('Build') {
    withMaven(jdk: 'java', maven: 'maven') {
        
        println "build is running"
        sh 'mvn -f pom.xml clean package -Dmaven.test.skip=true'
    }
}


stage('Build Image'){
    sh """        
        docker build -t springboot:1.0.0 .
        docker tag springboot:1.0.0 leenatejababu/springboot:1.0.0
        docker login -u leenatejababu -p ltb@11041986 
        docker push springboot:1.0.0 leenatejababu/springboot:1.0.0  
       """
}
}
