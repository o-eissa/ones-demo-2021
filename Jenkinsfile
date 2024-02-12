pipeline {
    agent any
    tools {
        go 'go-1.21'
    }
    environment {
        GO121MODULE = 'on'
    }
    stages {
        stage('Build') {
            environment {
                IMAGE_TAG = "value$BUILD_NUMBER"
            }
            steps {
                sh 'go build -o cmd/creator/creator-demo ./cmd/creator'
                sh 'go build -o cmd/mutator/mutator-demo ./cmd/mutator'
                sh 'go build -o cmd/transitor/transitor-demo ./cmd/transitor'
            }
        }
        // stage('Test') {
        //     steps {
        //         sh 'go test -cover ./...'
        //         sh 'go vet ./...'
        //         sh 'gofmt -l .'
        //         sh '[ "`gofmt -l .`" = "" ]'
        //     }
        // }
        stage('Run') {
            steps {
                sh 'cd scripts/bin && ./launch-mqtt.sh'
            }
        }
    }
}