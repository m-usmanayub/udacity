node {
    def registry = 'm-usman/udacity-project'
    stage ('Git Repo Checkout') {
        echo "Git Repo Checkout"
        checkout scm
        echo "Checkout complete"
    }
    
        stage('Build Image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("musmanayub/myudacityproject")
        echo "Build Complete"
        sh 'docker image ls'
}
