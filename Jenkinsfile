
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'mvn clean package'
                sh 'mvn --version'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
        stage('No-op') {
            steps {
                sh 'ls'
            }
        }
    }
     post {
    /*
     * These steps will run at the end of the pipeline based on the condition.
     * Post conditions run in order regardless of their place in pipeline
     * 1. always - always run
     * 2. changed - run if something changed from last run
     * 3. aborted, success, unstable or failure - depending on status
     */
        always {
            echo "I AM ALWAYS first"
             deleteDir()
        }
        changed {
            echo "CHANGED is run second"
        }
        aborted {
          echo "SUCCESS, FAILURE, UNSTABLE, or ABORTED are exclusive of each other"
        }
        success {
            echo "SUCCESS, FAILURE, UNSTABLE, or ABORTED runs last"
            mail to: 'blaisesianidev@gmail.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
        }
        unstable {
          echo "SUCCESS, FAILURE, UNSTABLE, or ABORTED runs last"
        }
        failure {
            mail to: 'blaisesianidev@gmail.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
            echo "SUCCESS, FAILURE, UNSTABLE, or ABORTED runs last"
        }
    }
}
