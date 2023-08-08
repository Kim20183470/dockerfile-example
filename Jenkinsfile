pipeline{
    agent any
    
    triggers{
        githubPush()
    }
    
    options{
        timestamps()
    }
    
    stages{
        stage('Github Clone & Checkout'){
            steps{
                git branch: 'main',
                url: 'https://github.com/Kim20183470/dockerfile-example.git'
            }
        }
        stage('Docker Build-ubuntu_apache2'){
            steps{
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub' ){
                    docker.build('dhu1758/ubuntu_apache2-test', './ubuntu_apache2')
                    }
                }
            }
        }
        stage('Docker Build-ubuntu_nginx'){
            steps{
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub' ){
                    docker.build('dhu1758/ubuntu_nginx-test', './ubuntu_nginx')
                    }
                }
            }
        }
        stage('Docker Build-ubuntu_nginx_loadbalancer'){
            steps{
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub' ){
                    docker.build('dhu1758/ubuntu_nginx_loadbalancer-test', './ubuntu_nginx_loadbalancer')
                    }
                }
            }
        }        
        stage('Docker Image Push'){
            steps{
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub' ){
                    def img = docker.image('dhu1758/ubuntu_apache2-test')
                    img.push('0.1')
                    }
                }
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub' ){
                    def img = docker.image('dhu1758/ubuntu_nginx-test')
                    img.push('0.1')    
                    }
                }
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub' ){
                    def img = docker.image('dhu1758/ubuntu_nginx_loadbalancer-test')
                    img.push('0.1')    
                    }
                }
            }          
        }
    }
    
    post{
        cleanup{
            emailext subject: '$DEFAULT_SUBJECT',
            to: 'cookie175858@gmail.com',
            body: '$DEFAULT_CONTENT'
            cleanWs()
        }
    }
}