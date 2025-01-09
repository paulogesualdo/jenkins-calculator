pipeline {
    agent any
    parameters {  
        string(name: 'operation', defaultValue: '+', description: 'Type + for addition or - for subtraction. Leave in blank for addition.')  
    } 

    stages {

        stage('Show current total') {
            steps {
                echo 'The current total is: XXXX'
            }
        }

        stage('Check operation') {
            steps {          
                script {
                    if (params.operation == '+') operationName = 'addition'
                    else if (params.operation == '-') operationName = 'subtraction'
                    else operationName = 'unknown'
                    echo "The operation chosen is: ${operationName}"
                }
            }
        }
        stage('Input value') {
            steps {
                echo 'Please type the value: XXXX'
            }
        }

        stage('Call calculador pipeline') {
            steps {
                echo 'Calling calculator pipeline'
            }
        }

        stage('Show the new value') {
            steps {
                echo 'The new value is: XXXX'
            }
        }
    }
}