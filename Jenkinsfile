// Declare global variables, shared between the stages
def existingHistoryContent = ""
def firstValueNumber
def operationName
def secondValueNumber
def total

pipeline {
    agent any
    parameters {  
        string (name: 'firstValueString', description: 'Type the first value.')
        choice (name: 'operation', choices: ['+', '-'], description: 'Choose + for addition or - for subtraction.')
        string (name: 'secondValueString', description: 'Type the second value.')
        booleanParam (name: 'showHistory', defaultValue: true, description: 'Select the checkbox to show calculation history')
    } 

    stages {

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

        stage('Convert values') {
            steps {          
                script {
                                        
                    // Try to convert the values from string to float. In case of failure, fail the pipeline showing an error message. The values were received as strings because it is not possible to receive them directly as floats. It would be possible to receive them as integers

                    try {
                        firstValueNumber = firstValueString.toFloat()
                    }
                    catch (NumberFormatException e) {
                        error "Invalid number format: ${firstValueString}"
                    }

                    try {
                        secondValueNumber = secondValueString.toFloat()
                    }
                    catch (NumberFormatException e) {
                        error "Invalid number format: ${secondValueString}"
                    }
                }
            }
        }

        stage('Call calculator pipeline') {
            steps {
                script {
                    
                    // Execute the operation
                    if (operationName == 'addition') total = firstValueNumber + secondValueNumber    
                    else if (operationName == 'subtraction') total = firstValueNumber - secondValueNumber
                }
            }
        }

        stage('Show the total') {
            steps {
                script {
                    
                    // Show the total on the console
                    if (operationName == 'addition') echo "${firstValueNumber} + ${secondValueNumber} = ${total}"
                    else if (operationName == 'subtraction')echo "${firstValueNumber} - ${secondValueNumber} = ${total}"
                }
            }
        }

        stage('Store on calculations history') {
            steps {
                script {
                    
                    // Declare variables
                    def newHistoryContent

                    // Store the calculation on newHistoryContent variable
                    if (operationName == 'addition') newHistoryContent = "${firstValueNumber} + ${secondValueNumber} = ${total}\n"
                    else if (operationName == 'subtraction') newHistoryContent = "${firstValueNumber} - ${secondValueNumber} = ${total}\n"

                    // Store the calculation on a history file. Create the file if it does not exist
                    try {
                        existingHistoryContent = readFile 'history.txt'
                    } catch (Exception e) {
                        echo "History file does not exist yet. Creating a new one."
                    }
                    writeFile file: 'history.txt', text: existingHistoryContent + newHistoryContent
                }
            }
        }        

        stage('Show the calculation history') {
            steps {
                script {
                    if (params.showHistory == true) {
                        existingHistoryContent = readFile 'history.txt'
                        echo "Calculation history:\n${existingHistoryContent}"
                    }
                    else echo "The user chose not to show the calculation history"
                }
            }
        }        
    }
}