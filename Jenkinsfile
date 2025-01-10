pipeline {
    agent any
    parameters {  
        string(name: 'firstValue', description: 'Type the first value.')
        string(name: 'operation', description: 'Type + for addition or - for subtraction.')
        string(name: 'secondValue', description: 'Type the first value.')  
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
                    
                    // Check if the parameter is "+" or "-". Fail the pipeline if it doesn't match any of the values
                    if (params.operation == '+') operationName = 'addition'
                    else if (params.operation == '-') operationName = 'subtraction'
                    else error("The operation chosen is unknown")
                    
                    // Show the operation name on the console
                    echo "The operation chosen is: ${operationName}"
                }
            }
        }

        stage('Call calculator pipeline') {
            steps {
                script {
                    
                    // Execute the operation
                    if (operationName == 'addition') total = firstValue + secondValue    
                    else if (operationName == 'subtraction') total = firstValue - secondValue
                }
            }
        }

        stage('Show the total') {
            steps {
                script {
                    
                    // Show the total on the console
                    if (operationName == 'addition') echo "${firstValue} + ${secondValue} = ${total}"
                    else if (operationName == 'subtraction')echo "${firstValue} - ${secondValue} = ${total}"
                }
            }
        }
    }
}