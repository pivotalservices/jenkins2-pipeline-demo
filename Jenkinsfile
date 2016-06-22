#!groovy

echo "Starting workflow"

stage 'build'
node {

    echo "Cloning Project"
    git 'https://github.com/dave-malone/spring-boot-personal-financier.git'

    echo "Building the Project with Gradle Wrapper"
    sh './gradlew build -x test'

    echo "Archiving Jar file"
    archive 'build/libs/*.jar'
}

stage 'test'
node {
    sh './gradlew clean test'
    step([$class: 'JUnitResultArchiver', testResults: '**/build/test-results/TEST-*.xml'])
}
