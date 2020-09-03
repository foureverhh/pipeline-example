pipeline{
    agent any
    parameters{
        choice (name:'DEPLOY_ENV',choices:['int','stage','prod'],description:'Target environment')
    }
    stages {
        stage('Build application'){
            agent any
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Deploy applicaiton'){
            agent any
            steps {
                sh 'mvn -v'
            }
        }


    }
}