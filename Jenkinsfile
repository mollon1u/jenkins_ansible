


pipeline{
    
    environment {
       IMAGE_NAME = "django"
       IMAGE_TAG = "latest"
    }
    agent none
    stages {
      stage("build"){
        agent any
        steps {
          sh """
            ssh vagrant@192.168.99.10
            sudo su
            cd TP2
            ansible-playbook -i hosts.INI deploy-webapp.yaml

             """
        }
      }
      stage("run"){
        agent any
        steps{
          script{
            sh '''
               ls /usr/bin
#               yum install docker-compose-1.18.0-4.el7.noarch
               docker build .
               ssh vagrant@192.168.99.11 -C \'sudo docker-compose -f /root/projet/projet-groupe-4/docker-compose.yml up -d'
	       sleep 50
               '''
          }
        }
      }
      stage('Test image') {
        agent any
        steps {
          script {
            sh '''
                curl -L "http://192.168.99.11:8000"
               '''
          }
        }
      }
    }
}