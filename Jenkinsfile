pipeline {
    agent none //any
    stages {
        stage('build') {
            steps {
                echo "They're grrrrreat!"
            }
        }
        stage('SonarQube Analysis') {
        	steps {
        		try {
            		def sqScannerMsBuildHome = tool 'sonarScannerMSBuild' //defined here http://localhost:8080/configureTools/
            		def msBuildHome = "C:\Program Files (x86)\MSBuild\14.0\Bin"
            		def slnHome = "C:\CodedUITesting"

    				withSonarQubeEnv('sonar') { //sonar defined here http://localhost:8080/configure
				      // Due to SONARMSBRU-307 value of sonar.host.url and credentials should be passed on command line
				      bat "${sqScannerMsBuildHome}\\SonarQube.Scanner.MSBuild.exe begin /k:CodedUI /n:CodedUITesting /v:1.0 /d:sonar.host.url=%SONAR_HOST_URL% /d:sonar.login=%SONAR_AUTH_TOKEN%"
				      bat "${msBuildHome}\\MSBuild.exe ${slnHome} /t:Rebuild"
				      bat "${sqScannerMsBuildHome}\\SonarQube.Scanner.MSBuild.exe end"
				    }
    			} 
    			catch(error) {
            		echo "The sonar server could not be reached ${error}"
        		}
        	}
        }
    }
    post {
        always {
            step([$class: 'LogParserPublisher', failBuildOnError: true, parsingRulesPath: 'C:\\Program Files (x86)\\Jenkins\\parsing_rules_example.txt', showGraphs: true, unstableOnWarning: true, useProjectRule: false])
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
