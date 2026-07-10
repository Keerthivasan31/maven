pipeline {
agent any
tools {
maven 'Maven-3.9'
jdk 'jdk17'
}
stages {
stage('Checkout') {
steps {
git branch: 'main',
url: 'https://github.com/Keerthivasan31/maven.git'
}
}
stage('Build') {
steps {
sh 'mvn clean compile'
}
}
stage('Test') {
steps {
sh 'mvn test'
}
post {
always {
junit 'target/surefire-reports/*.xml'
}
}
}
stage('Package') {
steps {
sh 'mvn package'
}
}
stage('Archive') {
steps {
archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
}
}
}
post {
success {
echo 'Pipeline completed successfully!'
}
failure {
echo 'Pipeline failed. Check console output above.'
}
}
}