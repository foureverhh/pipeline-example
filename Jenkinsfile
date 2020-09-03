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
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    
                    publishHTML([
                        allowMissing: false, 
                        alwaysLinkToLastBuild: false, 
                        keepAll: false,
                        reportDir: 'target/surefire-reports/', 
                        reportFiles: 'index.html',
                        reportName: 'Unit tests',
                        reportTitles: 'Unit tests'
                    ])
                    
                    publishHTML([
                        allowMissing: false, 
                        alwaysLinkToLastBuild: false,
                        keepAll: false, 
                        reportDir: 'target/site/jacoco/', 
                        reportFiles: 'index.html',
                        reportName: 'Tests Coverage', 
                        reportTitles: 'Tests Coverage'
                    ])
                }
                
                success {
                    archive 'target/calc-jsf-1.0.war'
                }
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