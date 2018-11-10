pipeline {
    agent any //none    

    stages {
        stage('build') {
            steps {
                echo "Build Stage"
            }
        }
        stage('SonarQube Analysis') {
        	steps {
	        	echo "SonarQube Analysis Stage"
	        	withSonarQubeEnv('sonar') { //sonar defined here http://localhost:8080/configure
				      // Due to SONARMSBRU-307 value of sonar.host.url and credentials should be passed on command line
				      bat "C:\\sonar-scanner-msbuild-4.3.1.1372-net46\\SonarQube.Scanner.MSBuild.exe begin /k:CodedUI /n:CodedUITesting /v:1.0 /d:sonar.host.url=%SONAR_HOST_URL%"
				      bat "C:\\Program Files (x86)\\MSBuild\\14.0\\Bin\\MSBuild.exe C:\\CodedUITesting /t:Rebuild"
				      bat "C:\\sonar-scanner-msbuild-4.3.1.1372-net46\\SonarQube.Scanner.MSBuild.exe end"
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
