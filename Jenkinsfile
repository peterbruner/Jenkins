pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "They're grrrrreat!"
            }
        }
    }
    post {
        always {
            step([$class: 'LogParserPublisher', failBuildOnError: true, showGraphs: true, unstableOnWarning: true, useProjectRule: false])
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
