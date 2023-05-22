
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Clean and install the project
                sh 'mvn spring-boot:run'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Wait') {
            steps {
                // Wait for 30 seconds before running the load test
                sh 'sleep 30'
            }
        }
        stage('Load test') {
            steps {
                // Run the SoapUI load test
                bat 'loadtestrunner.bat -s"http://localhost:8081 TestSuite" -c"Signup TestCase" -l"LoadTest 1" -m60 -n5 -r -f"C:\\Users\\Jose\\Downloads\\Programacion\\Codigos\\SOAPUi test" "C:\\Users\\Jose\\Downloads\\Programacion\\Codigos\\SOAPUi test\\REST-Project-1-soapui-project.xml"'
               //bat 'loadtestrunner.bat -s"http://localhost:8081 TestSuite" -c"Signup TestCase" -l"LoadTest 1" -m60 -n5 -r -f"C:/Users/Jose/Downloads/Programación/Códigos/SOAPUi test" -R -J-Dsoapui.export.pdf="C:/Users/Jose/Downloads/Programación/Códigos/SOAPUi_test/LoadTestReport.pdf" "C:/Users/Jose/Downloads/Programación/Códigos/SOAPUi test/REST-Project-1-soapui-project.xml"'
            }
        }
       
    }
}


