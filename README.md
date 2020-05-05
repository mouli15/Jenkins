# Jenkins
usernamePassword:
If your credentials ID is "USER_PASSWORD", you have to read it using eg. the following command: USER_CREDENTIALS = credentials('USER_PASSWORD'). After doing this, the username and password are available in the following environment variables: USER_CREDENTIALS_USR and USER_CREDENTIALS_PSW. Jenkins always adds _USR and _PSW endings to the names of the variables.
Example pipeline (I did not fully tested it, but should work):
pipeline {
    agent any

    environment {
        USER_CREDENTIALS = credentials('USER_PASSWORD')
    }

    stages {
        stage('Run') {
            steps {
                sh "echo $USER_CREDENTIALS_USR"
                sh "echo $USER_CREDENTIALS_PSW"
            }
        }
    }
}
If you get **** (four asterisks) as output, it's ok - Jenkins automatically masks usernames and passwords in the console output.

