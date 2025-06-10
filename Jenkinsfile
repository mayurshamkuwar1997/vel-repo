pipeline {
agent any 
  stages{
    stage{
      steps('cloning-repository') {
        dir(/mnt/project-1){
            sh ' rm -rf * '
             checkout scm
        }
      }
    }
     stage {
       steps ('making container and image') {
            sh 'docker run -dp 90:80 --name httpd-2 httpd'
       }
     }
    stage {
      steps('copying index.html in container) {
        dir('/mnt/project-1') {
          sh 'docker cp index.html httpd-2:/usr/local-apache2/htdocs'
        }
      }
    }
      stage{
        steps ('login into container ') {
         sh 'docker exec httpd-2 bash -c "chmod 777 /usr/local-apache2/htdocs/index.html"'
        }
      }
  }
}
