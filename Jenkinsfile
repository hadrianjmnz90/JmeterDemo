pipeline {
    agent any

    environment {
        // Surround with double quotes to handle space in "Program Files"
        JMETER_HOME = '"C:\\Program Files\\apache-jmeter-5.6.3"'
        PATH = "${JMETER_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Run JMeter Test') {
            steps {
                bat 'jmeter -n -t TestPlan_JpetStore.jmx -l results.jtl -e -o HTMLReport'
            }
        }

        stage('Publish Report') {
            steps {
                publishHTML(target: [
                    reportDir: 'HTMLReport',
                    reportFiles: 'index.html',
                    reportName: 'JMeter Report'
                ])
            }
        }
    }
}
