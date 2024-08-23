
pipeline {
    agent {
        label "jenkins-agent"
    }

    tools {
        jdk 'JDK17'
        maven 'MAVEN3'
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout form SCM") {
            steps {
                git branch: 'main',
                // credentialsId: 'github',
                url: 'https://github.com/dengyouf/springboot-app.git'
            }
        }

        stage("Build Application") {
            steps {
                sh'mvn clean package'
            }
        }

        stage("Test Application") {
            steps {
                sh'mvn test'
            }
        }
		
	stage("Sonarqube Analysis") {
            steps {
		withSonarQubeEnv(credentialsId: 'sonar-jenkins-ci-token') {
		    sh'mvn sonar:sonar'
		}
            }
        }
    }
}

