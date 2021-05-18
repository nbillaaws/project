pipeline {
    agent any

    stages {
        stage('Validate') {
            steps {
                echo 'validating..'
		sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
		sh 'mvn test'
		sh 'mvn test sonar:sonar -Dsonar.host.url=http://18.205.246.193:9000 -Dsonar.login=5c08c8abefefb3e290ac2f28d386a876c15cae10'    
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
		deploy adapters: [tomcat7(credentialsId: 'deploy', path: '', url: 'http://18.205.246.193:9090/')], contextPath: 'calculator', onFailure: false, war: '**/*.war'
            }
        }
    }
}
