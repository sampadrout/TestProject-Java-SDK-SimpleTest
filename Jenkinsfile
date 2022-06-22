pipeline {
    agent any
    environment {
        TP_DEV_TOKEN = credentials('71tH-tyQRbWL-gZCfrhZWBEPha_v-AGyu1aJGwBnQEY1')
        TP_API_KEY = credentials('Ho02kNu43ebT4d_MLk7RqKhSxh15YnWLGy3YAK7DKj41')
    }
    stages {
        stage('Run Agent on docker'){
            steps {
                //Download docker compose file from repo
                sh 'curl.exe --output docker-compose.yml --url https://raw.githubusercontent.com/testproject-io/python-sdk/master/.github/ci/docker-compose.yml'
                // Verify we use the updated latest 0.63.6 at least
                sh 'docker pull testproject/agent:latest'
                // Remove if exists
                sh 'docker-compose down'
                sh 'docker-compose -f docker-compose.yml up -d'
            }
        }
        stage('Run Test') {
            steps {
                script {
                    // Extra wait for agent on docker become a ready
                    sleep(time: 30, unit: "SECONDS")
                    // Run the test
                    sh "${tool 'Gradle'} test"
                }
            }
        }
    }
}