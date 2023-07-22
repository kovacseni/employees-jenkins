pipeline {
    environment {
//             DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
            VERSION_NUMBER = sh (
                                script: './mvnw help:evaluate -Dexpression=project.version -Dbuild.number=${BUILD_NUMBER} -q -DforceStdout',
                                returnStdout: true).trim()
            IMAGE_NAME = "kovacseni/employees:${VERSION_NUMBER}"
//             SONAR_CREDENTIALS = credentials('sonar-credentials')
    }
//     agent {
//         docker {
//             image 'eclipse-temurin:17'
//         }
//     }
    agent {
        dockerfile {
            filename 'Dockerfile.build'
            args '-e DOCKER_CONFIG=./docker'
        }
    }
    stages {
        stage('Commit') {
            steps {
                echo "Commit stage"
//                 sh "./mvnw -B clean package -Dbuild.number=${BUILD_NUMBER}"
            }
        }
        stage('Acceptance') {
             steps {
                 echo "Acceptance stage"
//                  sh "./mvnw -B integration-test -Dbuild.number=${BUILD_NUMBER}"
            }
        }
        stage('Docker') {
            steps {
                echo "Build and push Docker image"
//                 sh "docker build -f Dockerfile.layered -t ${IMAGE_NAME} ."
//                 sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u=${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
//                 sh "docker push ${IMAGE_NAME}"
//                 sh "docker tag ${IMAGE_NAME} kovacseni/employees:latest"
//                 sh "docker push kovacseni/employees:latest"
            }
        }
        stage('Quality') {
            parallel {
                stage('E2E API') {
                    steps {
                        echo "E2E API tests stage"
        //                 dir('employees-postman') {
        //                     sh 'rm -rf reports'
        //                     sh 'mkdir reports'
        //                     sh 'docker compose -f docker-compose.yaml -f docker-compose.jenkins.yaml up --abort-on-container-exit'
        //                     archiveArtifacts artifacts: 'reports/*.html', fingerprint: true
        //                 }
                    }
                }
                stage('Code quality') {
                      steps {
                          echo "Code quality"
        //                   sh "./mvnw sonar:sonar -Dsonar.host.url=http://host.docker.internal:9000 -Dsonar.login=${SONAR_CREDENTIALS_PSW}"
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy"
//             agent {
//                 dockerfile {
//                     filename 'Dockerfile.ansible'
//                 }
//             }
//             steps {
//                 script {
//                     env.DEFAULT_LOCAL_TMP = env.WORKSPACE_TMP
//                     env.HOME = env.WORKSPACE
//                 }
//                 sshagent(credentials : ['aws-credentials']) {
//                     sh "ansible-playbook docker-playbook.yaml -i inventory.yaml -e imageName=${IMAGE_NAME}"
//                 }
//             }
            }
        }
    }
}