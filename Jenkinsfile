pipeline {
    agent any
<<<<<<< HEAD
<<<<<<< HEAD
=======
<<<<<<< HEAD
=======
>>>>>>> ec722ae (Add actual project files)
    
    tools {
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
        IMAGE_TAG = "v${BUILD_NUMBER}"
    }
<<<<<<< HEAD
=======
>>>>>>> b8ade81 (Initial commit)
>>>>>>> 55a34ea (Initial commit)
=======
>>>>>>> ec722ae (Add actual project files)

    stages {
        stage('Git Checkout') {
            steps {
<<<<<<< HEAD
<<<<<<< HEAD
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/jaiswaladi246/Mega-Project-CD.git'
=======
<<<<<<< HEAD
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/jaiswaladi246/Mega-Project-CI.git'
>>>>>>> 55a34ea (Initial commit)
            }
        }
        
        stage('Kubernetes Deployment') {
            steps {
<<<<<<< HEAD
=======
=======
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/jaiswaladi246/Mega-Project-CI.git'
            }
        }
        
        stage('Compile') {
            steps {
>>>>>>> ec722ae (Add actual project files)
                sh "mvn compile"
            }
        }
        
        stage('Testing') {
            steps {
                sh "mvn test"
            }
        }
        
        stage('Trivy FS Scan') {
            steps {
                sh "trivy fs --format table -o fs-report.html ."
            }
        }
        
        stage('Sonar Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh '''
                        $SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.projectKey=gcbank \
                        -Dsonar.projectName=gcbank \
                        -Dsonar.java.binaries=target
                    '''
                }
            }
        }
        
        stage('Quality Gate Check') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
        
        stage('Build') {
            steps {
                sh "mvn package"
            }
        }
        
        stage('Publish To Nexus') {
            steps {
                withMaven(globalMavenSettingsConfig: 'devopsshack', maven: 'maven3', traceability: true) {
                    sh "mvn deploy"
                }
            }
        }
        
        stage('Docker Image Build & Tag') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        sh "docker build -t adijaiswal/bankapp:$IMAGE_TAG ."
                    }
                }
            }
        }
        
        stage('Scan Image') {
            steps {
                sh "trivy image --format table -o image-report.html adijaiswal/bankapp:$IMAGE_TAG"
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        sh "docker push adijaiswal/bankapp:$IMAGE_TAG"
                    }
                }
            }
        }
        
        stage('Update Manifest File in Mega-Project-CD') {
            steps {
                script {
                    // Clean workspace before starting
                    cleanWs()

                    withCredentials([usernamePassword(credentialsId: 'git', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                        sh '''
                            # Clone the Mega-Project-CD repository
                            git clone https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/jaiswaladi246/Mega-Project-CD.git
                            
                            # Update the image tag in the manifest.yaml file
                            cd Mega-Project-CD
                            sed -i "s|adijaiswal/bankapp:.*|adijaiswal/bankapp:${IMAGE_TAG}|" Manifest/manifest.yaml
                            
                            # Confirm changes
                            echo "Updated manifest file contents:"
                            cat Manifest/manifest.yaml
                            
                            # Commit and push the changes
                            git config user.name "Jenkins"
                            git config user.email "jenkins@example.com"
                            git add Manifest/manifest.yaml
                            git commit -m "Update image tag to ${IMAGE_TAG}"
                            git push origin main
                        '''
                    }
<<<<<<< HEAD
=======
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/jaiswaladi246/Mega-Project-CD.git'
            }
        }
        
        stage('Kubernetes Deployment') {
            steps {
>>>>>>> 55a34ea (Initial commit)
                withKubeConfig(caCertificate: '', clusterName: 'devopsshack-cluster', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://952FB702C508F688D873376083B31DF5.gr7.ap-south-1.eks.amazonaws.com') {
                    sh "kubectl apply -f Manifest/manifest.yaml -n webapps"
                    sh "kubectl apply -f Manifest/HPA.yaml "
                    sleep 30
                    sh "kubectl get pods -n webapps"
                    sh "kubectl get service -n webapps"
<<<<<<< HEAD
=======
>>>>>>> b8ade81 (Initial commit)
>>>>>>> 55a34ea (Initial commit)
=======
>>>>>>> ec722ae (Add actual project files)
                }
            }
        }
    }
<<<<<<< HEAD
<<<<<<< HEAD
=======
<<<<<<< HEAD
=======
>>>>>>> ec722ae (Add actual project files)
    
    
post {
    always {
        script {
            def jobName = env.JOB_NAME
            def buildNumber = env.BUILD_NUMBER
            def pipelineStatus = currentBuild.result ?: 'UNKNOWN'
            def bannerColor = pipelineStatus.toUpperCase() == 'SUCCESS' ? 'green' : 'red'

            def body = """
                <html>
                <body>
                <div style="border: 4px solid ${bannerColor}; padding: 10px;">
                <h2>${jobName} - Build ${buildNumber}</h2>
                <div style="background-color: ${bannerColor}; padding: 10px;">
                <h3 style="color: white;">Pipeline Status: ${pipelineStatus.toUpperCase()}</h3>
                </div>
                <p>Check the <a href="${BUILD_URL}">console output</a>.</p>
                </div>
                </body>
                </html>
            """

            emailext (
                subject: "${jobName} - Build ${buildNumber} - ${pipelineStatus.toUpperCase()}",
                body: body,
                to: '567adddi.jais@gmail.com',
                from: 'jenkins@devopsshack.com',
                replyTo: 'jenkins@devopsshack.com',
                mimeType: 'text/html',
               
            )
        }
    }
}
<<<<<<< HEAD
=======
>>>>>>> b8ade81 (Initial commit)
>>>>>>> 55a34ea (Initial commit)
=======
>>>>>>> ec722ae (Add actual project files)
}
