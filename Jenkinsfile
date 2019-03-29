pipeline {
    agent any
    stages {
        stage ("Build") {
            steps {
                sh 'chmod u+x ./build/*.sh'
                sh './build/clean.sh'
                sh './build/build.sh'
                sh './build/tag.sh'
                withDockerRegistry([ credentialsId: "docker-hub", url: "https://secure.gravatar.com/avatar/a45ce90799d347b9db6c50a8a2ec7e24.jpg?s=80&r=g&d=mm" ]) {
                    sh './build/push.sh'
                }

                sh 'chmod u+x ./test/project/*.sh'
                sh 'cd ./test/project && ./run_chrome.sh'
                sh 'cd ./test/project && ./run_chrome_advanced.sh'
                sh 'cd ./test/project && ./run_firefox.sh'
                archiveArtifacts '**/*.avi'
            }
        }
    }
}