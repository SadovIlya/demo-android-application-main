pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:    
          containers:                      
          - name: fastlane
            image: fastlanetools/fastlane
            command:
            - cat
            tty: true       
        '''
    }
  }
  stages {
    stage('fastlane') {
      steps {
        container('fastlane') {
          sh 'fastlane beta'
        }
      }
    }

  }
}