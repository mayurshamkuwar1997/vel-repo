pipeline {
    agent any
    stages {
        stage('Cloning Repository') {
            steps {
                dir('/mnt/project-2') {
                    sh 'rm -rf *'
                    checkout scm
                }
            }
        }

        stage('Making Container and Image') {
            steps {
                sh 'docker system prune -a -f'
                sh 'docker run -dp 91:80 --name httpd-3 httpd'
            }
        }

        stage('Copying index.html into Container') {
            steps {
                dir('/mnt/project-2') {
                    sh 'docker cp index.html httpd-3:/usr/local/apache2/htdocs'
                }
            }
        }

        stage('Login into Container and Set Permissions') {
            steps {
                sh 'docker exec httpd-3 bash -c "chmod 777 /usr/local/apache2/htdocs/index.html"'
            }
        }
    }
}
