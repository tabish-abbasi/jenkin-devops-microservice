node {
    // Set environment variables
    def dockerHome = tool 'myDocker'  // Assuming 'myDocker' is the ID of the Docker installation in Jenkins
    def mavenHome = tool 'myMaven'    // Assuming 'myMaven' is the ID of the Maven installation in Jenkins
    env.PATH = "${dockerHome}/bin:${mavenHome}/bin:${env.PATH}"

    stage('Compile') {
        // Compile stage steps
        sh 'echo "Using Docker at: ${dockerHome}"'
        sh 'echo "Using Maven at: ${mavenHome}"'
        sh 'mvn --version'  // Confirm Maven setup
        sh 'docker --version'  // Confirm Docker setup
        sh 'mvn clean compile'  // Compile the project
    }
}
