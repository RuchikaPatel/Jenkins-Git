pipeline {
    agent any 
    environment{
        NEW_VERSION = '1.3.0'
        // using credential in jenkins file "credential("credentialID")" binds the credential to your env var
        SERVER_CREDENTIALS = credentials('server-credential')
    }   
    parameters{
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    stages {
        stage('Build') { 
            steps {
                echo 'building the application. ..'
                echo "building version ${NEW_VERSION}"
            }
        }
        stage('Test') {
            when{
                expression{
                    //BRANCH_NAME == 'dev' && BRANCH_NAME == 'main'
                    params.executeTest
                }    
            }
            steps {
                echo 'testing the application...'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'deploying the application...'
                echo "deploying versio $params.VERSION"
                withCredentials([
                    usernamePassword(credentials: 'server-credential', usernameVariable: USER, passwordVariable: PWD)
                ])
            }
        }
    }
}
