pipeline {
    agent any
    stages {
        stage('Cloning Repository') {
            steps {
                dir('/mnt/project') {
                    
                    sh 'rm -rf *'
                    
                    checkout scm
                }
            }
        }

        stage('Making Container and Image') {
            steps {
                sh '''
                docker kill httpd-1
                docker rm httpd-1
                docker volume rm abcd
                docker run -dp 80:80 --name httpd-1 httpd
                docker volume create abcd
                '''
                
            }
        }

        stage('Copying index.html into Container') {
            steps {
                dir('/mnt/project') {
                    sh 'docker cp index.html httpd-1:/usr/local/apache2/htdocs'
                }
            }
        }

        stage('Login into Container and Set Permissions') {
            steps {
                sh 'docker exec httpd-1 bash -c "chmod 777 /usr/local/apache2/htdocs/index.html"'
            }
        }
    }
}
