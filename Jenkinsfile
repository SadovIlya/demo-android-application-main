pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:    
          containers:                      
          - name: fastlane
            image: jungsoft/react-native-android-fastlane
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
          sh 'echo $JAVA_HOME'
          sh 'ls /usr/lib/jvm'
        }
      }
    }

  }
}
