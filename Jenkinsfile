def bucket = 'us-east-1-lambda-example'
def functionName = 'lambda-example'
def region = 'us-east-1'

node('slaves'){
   def root = tool name: 'Go 1.13', type: 'go'
    stage('Checkout'){
        checkout scm
    }

    stage('Command'){
        sh 'env'
    }

    stage('Version'){
      withEnv(["GOPATH=${env.WORKSPACE}/go", "GOROOT=${root}", "GOBIN=${root}/bin", "PATH+GO=${root}/bin"]) {
        sh "mkdir -p ${env.WORKSPACE}/go/src"
        sh 'go version'
        sh "go get -u golang.org/x/lint/golint"
        sh 'go get -t ./...'
        sh 'golint -set_exit_status'
        sh 'go vet .'
        sh 'go test .'
	}
    }

    stage('Build'){
        sh 'GOOS=linux go build -o main main.go'
        sh "zip ${commitID()}.zip main"
    }

    stage('Push'){
        sh "aws s3 cp ${commitID()}.zip s3://${bucket}"
    }

    stage('Deploy'){
        sh "aws lambda update-function-code --function-name ${functionName} \
                --s3-bucket ${bucket} \
                --s3-key ${commitID()}.zip \
                --region ${region}"
    }
}

def commitID() {
    sh 'git rev-parse HEAD > .git/commitID'
    def commitID = readFile('.git/commitID').trim()
    sh 'rm .git/commitID'
    commitID
}
