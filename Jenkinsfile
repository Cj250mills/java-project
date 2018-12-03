node('linux') {

stage('Unit Tests') {
sh 'ant -f test.xml -v'
junit 'reports/result.xml'
}

stage('Build') {
git 'https://github.com/Cj250mills/java-project.git'
sh 'ant -f build.xml -v'
}


stage('Report') {
withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',
                  accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '46e4c83d-f72e-46a0-bb36-6ede15737739', 
                  secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
}
}
}
