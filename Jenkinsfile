pipeline {
agent {
        docker {
            image 'maven:latest'
            args '-v /root/.m2:/root/.m2'
        }
}	
    stages {
        stage('Checkout') {
		steps {
            	git branch: 'master',
    		credentialsId: '9dcd8d46-9018-4abc-8c6c-d61cc1cf5e47',
    		url: 'git@github.com:AswiniVadlamudi/Jenkins.git'
		}
        }
        stage('Build') {
            steps {
                echo 'Clean Build'
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                sh 'mvn test'
            }
        }
        
        stage('Sonar') {
            steps {
                echo 'Sonar Scanner'
               	//def scannerHome = tool 'SonarQube Scanner 3.0'    
			sh "mvn sonar:sonar -Dsonar.host.url=http://35.227.88.186:9000"
            			
            }
	}
        
        stage('Package') {
            steps {
                echo 'Packaging'
                sh 'mvn package -DskipTests'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy'
		    sh 'mvn deploy'
            }
        }
    }
    
    post {
        always {
            echo 'JENKINS PIPELINE'
        }
        success {
            echo 'JENKINS PIPELINE SUCCESSFUL'
        }
        failure {
            echo 'JENKINS PIPELINE FAILED'
        }
        unstable {
            echo 'JENKINS PIPELINE WAS MARKED AS UNSTABLE'
        }
        changed {
            echo 'JENKINS PIPELINE STATUS HAS CHANGED SINCE LAST EXECUTION'
        }
    }
}
