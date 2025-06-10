pipeline {
agent any 
  stages{
    stage{
      steps('cloning-repository') {
        dir('/mnt/project'){
            sh ' rm -rf * '
             checkout scm
        }
      }
    }
     stage {
       steps ('making container and image') {
            sh 'docker run -dp 80:80 --name httpd-1 httpd'
       }
     }
    stage {
      steps('copying index.html in container') {
        dir('/mnt/project') {
          sh 'docker cp index.html httpd-1:/usr/local-apache2/htdocs'
        }
      }
    }
      stage{
        steps ('login into container ') {
         sh 'docker exec httpd-1 bash -c "chmod 777 /usr/local-apache2/htdocs/index.html"'
        }
      }
  }
}
