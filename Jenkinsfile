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
