pipeline {
    agent any
    stages {
        stage('Run Agent on docker'){
            steps {
                //Download docker compose file from repo
                // Verify we use the updated latest 0.63.6 at least
                // Remove if exists
                withEnv(["PATH=$PATH:/usr/local/bin"]){
                    sh 'docker-compose down'
                    sh 'docker-compose -f docker-compose.yml up -d'
                }
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