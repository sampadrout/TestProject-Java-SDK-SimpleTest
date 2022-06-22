pipeline {
    agent any
    stages {
        stage('Run Agent on docker'){
            steps {
                //Download docker compose file from repo
                sh 'curl.exe --output docker-compose.yml --url https://raw.githubusercontent.com/testproject-io/python-sdk/master/.github/ci/docker-compose.yml'
            }
        }
    }
}