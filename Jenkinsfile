pipeline {

    agent { label 'validation' }


    stages {
        stage ('GIT') {
            steps {
               echo "Getting Project from Git"; 
                git branch: "main", 
                    url: "https://github.com/FarjallahAhmed/Devops_Cours.git";
            }
        }
       
        stage("Build") {
            steps {
                sh "mvn clean package";
            }
        }
        
        stage("Sonar") {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login="admin" -Dsonar.password="vagrant"'
            }
        }
        
        stage("Build artifact") {
            steps {
                sh "sudo docker build -t tpachat .";
            }
        }
        
        stage("docker compose") {
            steps {
                sh "sudo docker compose up -d";
            }
        }
        stage('Deployment in nexus') {
            steps {
                sh 'mvn deploy -Dmaven.test.skip=true'
            }
        }
        
    }
   
    post {
        always {
            cleanWs()
        }
    }
    
}