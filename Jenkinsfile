


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
          pwd
          ls
            ssh -tt vagrant@192.168.99.10 /bin/bash <<'EOT'
            pwd
            ls
            sudo su
            cd TP2
            ansible-playbook -i hosts.INI deploy-webapp.yaml
            exit
            exit
            'EOT'
            pwd
             """
        }
      }

      stage('Test image') {
        agent any
        steps {
          script {
            sh '''
                curl -L "http://192.168.99.10"
               '''
          }
        }
      }
    }
}
