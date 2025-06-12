pipeline {
    agent any
    stages {
        stage('Cloning Repository') {
            steps {
                dir('/mnt/project-1') {
                    sh 'rm -rf *'
                    checkout scm
                }
            }
        }

        stage('Making Container and Image') {
            steps {
               sh ' docker run -dp 90:80 -v server:/usr/local/apache2/htdocs/ --name httpd-1 httpd '
            }
        }

        stage('Copying index.html into Container') {
            steps {
                dir('/mnt/project-1') {
                    sh 'docker cp index.html httpd-2:/usr/local/apache2/htdocs'
                }
            }
        }

        stage('Login into Container and Set Permissions') {
            steps {
                sh 'docker exec httpd-2 bash -c "chmod 777 /usr/local/apache2/htdocs/index.html"'
            }
        }
    }
}
