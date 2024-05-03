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
                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
            }
        }
        stage('Building Image') {
            steps {
                sh 'docker build -t azizabdellaoui/ski .'
            }
        }
        stage('Pushing Image') {
            steps {
                sh 'echo "Express*216" | docker login -u aziz1 --password-zdazizou10'
                sh 'docker tag azizabdellaoui/ski aziz1/ski-devops:latest'
                sh 'docker push aziz1/ski-devops:latest'
            }
        }

}