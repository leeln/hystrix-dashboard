node {
    stage 'build'
    checkout scm
    docker.image('leeln/java:jdk-8').inside {
        sh './gradlew build'
        archive 'build/libs/*.war'
    }

    stage 'push'
    docker.withRegistry('https://docker.repo.leeln.com', 'leeln-admin') {
        docker.build('leeln/hystrix-dashboard').push()
    }

    stage 'deploy'
    sh 'rancher up -s leeln -p -d -u -c'
}