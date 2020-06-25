node {
    def registry = 'musmanayub/udacity-project'
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
        app = docker.build(${registry})
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

stage('Deploying') {
      echo 'Deploying to AWS...'
      dir ('./') {
        withAWS(credentials: 'aws-jenkins', region: 'us-west-2') {
            sh "aws eks --region us-west-2 update-kubeconfig --name CapstoneEKSUdacity-0TtoHmzFVWVJ"
            sh "kubectl get nodes"
            sh "kubectl get pods"
            sh "kubectl apply -f aws/kube/aws-auth-cm.yaml"
            sh "kubectl apply -f aws/kube/depl.yml"
            sh "kubectl apply -f aws/kube/lb.yml"
            sh "kubectl get nodes"
            sh "kubectl get pods"
        }
}
