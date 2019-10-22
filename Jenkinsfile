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
        sh 'ls -l $HOME/workspace/example-lambda-master'
        sh 'env ${GOPATH}'
        sh 'env ${GOROOT}'
        sh 'go version'
	}
    }
    stage('File'){
        sh 'echo "machine https://github.com login ane4ka0205 password vfkfyjdf0205 > $HOME/.netrc"'
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
