node {
    // Set environment variables
    def dockerHome = tool 'myDocker'
    def mavenHome = tool 'myMaven'
    env.PATH = "${dockerHome}/bin:${mavenHome}/bin:${env.PATH}"

    stage('Compile') {
        // Compile stage steps
        sh 'echo "Using Docker: ${dockerHome}"'
        sh 'echo "Using Maven: ${mavenHome}"'
        sh 'mvn --version'  // Confirm maven setup
        sh 'docker --version'  // Confirm docker setup
        sh 'mvn clean compile'
    }

    // Add other stages as needed, using the same pattern
    // Example:
    stage('Package') {
        sh 'mvn package -DskipTests'
    }

    stage('Build Docker Image') {
        def dockerImage
        script {
            dockerImage = docker.build("tabishabbasi/currency-exchange-devops:${env.BUILD_NUMBER}")
        }
    }

    stage('Push Docker Image') {
        script {
            docker.withRegistry('', 'dockerhub') {
                dockerImage.push()
                dockerImage.push('latest')
            }
        }
    }
}

// Post actions
post {
    always {
        echo 'This will always run after the build.'
    }
    success {
        echo 'This runs if the build is successful.'
    }
    failure {
        echo 'This runs if the build fails.'
    }
}
