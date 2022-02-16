pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:    
          containers:    
          - name: docker
            image: docker:19.03.1-dind
            securityContext:
              privileged: true
            env: 
              - name: DOCKER_TLS_CERTDIR
                value: ""              
          - name: cli
            image: amazon/aws-cli
            command:
            - cat
            tty: true       
        '''
    }
  }
  stages {
    stage('cli') {
      steps {
        container('cli') {
          sh 'aws ecr get-login-password --region us-west-2 > 1.txt'
        }
      }
    }
    stage('docker') {
      steps {       
        container('docker') {
          sh 'docker login --username AWS --password-stdin  529396670287.dkr.ecr.us-west-2.amazonaws.com <1.txt'
          sh 'docker build -t 529396670287.dkr.ecr.us-west-2.amazonaws.com/sadov-ecr-frontend:latest .'         
          sh 'docker push 529396670287.dkr.ecr.us-west-2.amazonaws.com/sadov-ecr-frontend:latest'        
        }
      }
    }  
  }
}