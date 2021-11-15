pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                        userRemoteConfigs: [[
                            url: 'https://github.com/326-163/myapp.git']]])
                }
             }
         }



        stage('install') {
             steps{
                script{
                    sh "sudo npm install"
                }
            }
        }

        stage ('Build') {
   		steps {
			script {
			sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml "
	        }
            }
         }

        stage('docker') {
             steps{
                script{
                    sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml "
                }
            }
        }

        stage('dockerHub') {
             steps{
                script{
                    sh "ansible-playbook ansible/docker-registry.yml -i Ansible/inventory/host.yml"
                }
            }
        }


       }
      }
