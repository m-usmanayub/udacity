node {
    def registry = 'm-usman/udacity-project'
    stage ('Git Repo Checkout') {
        echo "Git Repo Checkout"
        checkout scm
        echo "Checkout complete"
    }
    
    stage("Linting") {
      echo 'Linting...'
      sh 'docker run --rm -i hadolint/hadolint < Dockerfile'
    }

        stage('Build Image') {
        app = docker.build("musmanayub/myudacityproject:v1")
        echo "Build Complete"
        sh 'docker image ls'
        }

        stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('', 'dockerhub') {
            app.push()
        echo 'Image pushed to Docker Hub'
        }
    }
    
}
