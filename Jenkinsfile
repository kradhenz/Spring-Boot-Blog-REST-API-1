
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Clean and install the project
                sh 'mvn clean install'
            }
        }
        stage('Start API') {
            steps {
                // Change directory to target
                dir('target/') {
                    // Run the jar in background and set port to 8081
                    sh 'java -jar blogapi-0.0.1-SNAPSHOT.jar  &'
                }
            }
        }
        stage('Wait') {
            steps {
                // Wait for 30 seconds before running the load test
                sh 'sleep 30'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Load test') {
            steps {
                // Run the SoapUI load test
                bat 'loadtestrunner.bat -s"http://localhost:8081 TestSuite" -c"Signup TestCase" -l"LoadTest 1" -m60 -n5 -r -f"C:\\Users\\Jose\\Downloads\\Programacion\\Codigos\\SOAPUi test" "C:\\Users\\Jose\\Downloads\\Programacion\\Codigos\\SOAPUi test\\REST-Project-1-soapui-project.xml"'
               //bat 'loadtestrunner.bat -s"http://localhost:8081 TestSuite" -c"Signup TestCase" -l"LoadTest 1" -m60 -n5 -r -f"C:/Users/Jose/Downloads/Programación/Códigos/SOAPUi test" -R -J-Dsoapui.export.pdf="C:/Users/Jose/Downloads/Programación/Códigos/SOAPUi_test/LoadTestReport.pdf" "C:/Users/Jose/Downloads/Programación/Códigos/SOAPUi test/REST-Project-1-soapui-project.xml"'
            }
        }
        stage('Release the port 8081') {
            steps {
                echo "El puerto se cierra automáticamente"
                 //bat 'for /f "tokens=5" %p in (\'netstat -ano ^| findstr :8081 ^| findstr LISTENING ^| findstr /r /c:" *[0-9]*$" \') do taskkill /f /pid %p > nul 2>&1'
                script {
                     def pid = bat(returnStdout: true, script: 'netstat -ano | findstr :8081').split("\\s+")[4]
                     bat "taskkill /pid ${pid} /f"
                    echo "El puerto 8081 ha sido liberado."
                 }                
            }
        }
    }
}





