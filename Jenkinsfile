pipeline {
//  agent any
    agent {label 'slave-1'}
    tools {
      nodejs 'NodeJS-20.0.0'
            }
    stages {
        stage('git-clone') {
            steps {
                git branch: 'main', credentialsId: 'Git_credentials', url: 'https://github.com/JayantH2o/Contact_frontend-app.git'
            }
        }
        stage ('NPM Build'){
            steps {
                sh 'npm version;npm install;npm -g @angular/cli;ng v;ng build'
                    }    
        
            }
    
        stage ('Build and push docker image'){
            steps{
                withCredentials([string(credentialsId: 'dockerAcntpwd', variable: 'dockerAcntpwd')]) {
                sh 'docker login -u jayachandrant -p ${dockerAcntpwd} '
                sh 'docker build -t jayachandrant/contact_ui_app .'
				sh 'docker push jayachandrant/contact_ui_app'
            }
        }   
        }


/* stage ('Deploy'){
            steps{
                sh 'kubectl apply -f Deployment.yml'
                sh 'kubectl get all -o wide'
               }
        }   */
        
    }
}
