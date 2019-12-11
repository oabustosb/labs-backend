pipeline {
    agent any
    tools {
        maven 'Maven'
        jdk 'JDK 1.8'
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    curl "https://api.github.com/repos/oabustosb/labs-backend/statuses/$GIT_COMMIT?access_token=a2796daefdb4cd194e67fb7ec4e468bdb18089ea" \
                      -H "Content-Type: application/json" \
                      -X POST \
                      -d "{\"state\": \"pending\",\"context\": \"continuous-integration/jenkins\", \"description\": \"Jenkins\", \"target_url\": \"$BUILD_URL\"}"
                '''
                sh '''
                    echo "PATH = ${PATH}"
                '''
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn clean install package spring-boot:repackage'
            }
        }
    }
    post{
        always{
            sh '''
                curl "https://api.github.com/repos/oabustosb/labs-backend/statuses/$GIT_COMMIT?access_token=a2796daefdb4cd194e67fb7ec4e468bdb18089ea" \
                  -H "Content-Type: application/json" \
                  -X POST \
                  -d "{\"state\": \"success\",\"context\": \"continuous-integration/jenkins\", \"description\": \"Jenkins\", \"target_url\": \"$BUILD_URL\"}"
            '''
        }
    }
}
