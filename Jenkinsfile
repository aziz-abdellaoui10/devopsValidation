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
                withSonarQubeEnv(installationName: 'sq1'){
                    sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
                }
                //sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
            }
        }
        stage('Building Image') {
            steps {
                sh 'docker build -t aziz1/ski .'
            }
        }
        stage('Pushing Image') {
            steps {
                sh 'echo "zdazizou10" | docker login -u aziz1 --password-stdin'
                sh 'docker tag aziz1/ski aziz1/ski-devops:latest'
                sh 'docker push aziz1/ski-devops:latest'
            }
        }
    }
}