pipeline {
agent any 
  stages{
    stage{
      steps('cloning-repository') {
        dir('/mnt/project-2'){
            sh ' rm -rf * '
             checkout scm
        }
      }
    }
     stage {
       steps ('making container and image') {
            sh 'docker run -dp 91:80 --name httpd-3 httpd'
       }
     }
    stage {
      steps('copying index.html in container) {
        dir('/mnt/project-2') {
          sh 'docker cp index.html httpd-3:/usr/local-apache2/htdocs'
        }
      }
    }
      stage{
        steps ('login into container ') {
         sh 'docker exec httpd-3 bash -c "chmod 777 /usr/local-apache2/htdocs/index.html"'
        }
      }
  }
}
