pipeline {
    agent any
    
    tools {
        maven 'maven'
        jdk 'jdk17'
        
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
        
    }
    
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AmalSunny992/ci-cd.git'
            }
        }
       
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('Unit Test') {
            steps {
                sh 'mvn test -DskipTests=true'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=EKART -Dsonar.projectName=EKART \
                    -Dsonar.java.binaries=.'''
                    
                }
            }
        }
 
        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'DC'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
  
        stage('Build') {
            steps {
                sh 'mvn package -DskipTests=true'
            }
        }
    
        stage('Deploy To Nexus') {
            steps {
                withMaven(globalMavenSettingsConfig: 'global-maven', jdk: 'jdk17', maven: 'maven', mavenSettingsConfig: '', traceability: true) {
                    sh "mvn deploy -DskipTests=true"
                }
            }
        }
        
        stage('Docker Build and Tag Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockertoken', toolName: 'docker') {
                        sh "docker build -t adijaiswal/ekart:latest -f docker/Dockerfile ."
                    }
                }
            }
        }
        
        stage('Trivy Scan') {
            steps {
                    sh "trivy image adijaiswal/ekart:latest > trivy-report.txt"
            }
        }
        
        stage('Docker Push Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockertoken', toolName: 'docker') {
                        sh "docker push amalsunny992/ekart:latest"
                    }
                }
            }
        }
        
    stage('Kubernetes Deploy') {
            steps {
                    withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://172.31.43.67:6443') {
                    sh "kubectl apply -f deploymentservice.yml -n webapps"
                    sh "kubectl get svc -n webapps "
                    }
            }
        }
    }
}
