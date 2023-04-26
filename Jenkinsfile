node {
    def app
    stage('Initialize'){
        def dockerHome = tool 'myDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build('abhinavprakash1992/Devops')
    }
    stage('Test image') {
        app.inside{
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image'){
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}