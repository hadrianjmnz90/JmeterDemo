pipeline {
    agent any

    environment {
        JMETER_HOME = 'C:\\Program Files\\apache-jmeter-5.6.3'
        PATH = "${JMETER_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Clean Old Report') {
            steps {
                bat 'rmdir /s /q HTMLReport || exit 0'
            }
        }
        stage('Run JMeter Test') {
            steps {
                bat '"%JMETER_HOME%\\bin\\jmeter.bat" -n -t TestPlan_JpetStore.jmx -l results.jtl -e -o HTMLReport'
            }
        }

        stage('Publish Report') {
            steps {
                publishHTML(target: [
                    allowMissing: true,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'HTMLReport',
                    reportFiles: 'index.html',
                    reportName: 'JMeter Report'
                ])
            }
        }
    }
}
