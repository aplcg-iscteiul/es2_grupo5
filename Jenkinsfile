def dockeruser = "jrlmc"
def imagenameMysql = "mysql"
def imagenameWordPress = "wordpress"
def container = "wordpress"

node {
   echo 'Building Apache Docker Image'

stage('Git Checkout') {
    git 'https://github.com/aplcg-iscteiul/ES2_Grupo5.git'
    }
    
stage('Build Docker Image'){
     powershell "docker-compose up -d"
    }
    
   stage('Stop Existing Container'){
     powershell "docker stop ${container}"
    }
    
stage('Remove Existing Container'){
     powershell "docker rm ${container}"
    }
    
stage ('Runing Container to test built Docker Image'){
   powershell "docker run -dit --name ${container} -p 80:80 ${imagenameMysql}"
    }
    
   stage ('Runing Container to test built Docker Image'){
      powershell "docker run -dit --name ${container} -p 80:90 ${imagenameWordPress}"
    }
   
stage('Tag Docker Image'){
    powershell "docker tag ${imagenameMysql} ${env.dockeruser}/mysql"
    }
   
   stage('Tag Docker Image'){
    powershell "docker tag ${imagenameWordPress} ${env.dockeruser}/wordpress"
    }

stage('Docker Login and Push Image'){
    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'dockerpasswd', usernameVariable: 'dockeruser')]) {
    powershell "docker login -u ${dockeruser} -p ${dockerpasswd}"
    }
    powershell "docker push ${dockeruser}/wordpress"
    }

}
}
