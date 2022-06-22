pipeline {
    agent any
    stages {
        stage('Run Agent on docker'){
            steps {
                //Download docker compose file from repo
                sh 'curl --output docker-compose.yml --url https://raw.githubusercontent.com/testproject-io/python-sdk/master/.github/ci/docker-compose.yml'
                // Verify we use the updated latest 0.63.6 at least
                sh "${tool 'Docker'} pull testproject/agent:latest"
                // Remove if exists
                sh "${tool 'Docker-compose'} down"
                sh "${tool 'Docker-compose'} -f docker-compose.yml up -d"
            }
        }
        stage('Run Test'){
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