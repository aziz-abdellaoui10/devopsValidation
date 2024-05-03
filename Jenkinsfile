pipeline {
    agent any
    stages {
        stage('MavenCompile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage(' Test JUnit') {
            steps {
                sh 'mvn test -Dtest=PisteServicesImplTest'
            }
        }
       stage('Maven Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }
        stage('Sonarqube') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar123'
            }
        }
        stage('Building Image') {
            steps {
                sh 'docker build -t azizabdellaoui/ski .'
            }
        }
        stage('Pushing Image') {
            steps {
                sh 'echo "Express*216" | docker login -u azizabd --password-stdin'
                sh 'docker tag azizabdellaoui/ski azizabd/ski-devops:latest'
                sh 'docker push azizabd/ski-devops:latest'
            }
        }

}