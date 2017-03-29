pipeline {
  agent any
  stages {
    stage('setup') {
      steps {
        sh 'apt-get -y install live-build qemu-user-static debootstrap make'
      }
    }
    stage('configure armhf') {
      steps {
        parallel(
          "configure armhf": {
            sh '''cd armhf
make clean
./configure'''
            
          },
          "configure arm64": {
            sh '''cd arm64
make clean
./configure'''
            
          }
        )
      }
    }
    stage('build armhf') {
      steps {
        parallel(
          "build armhf": {
            sh '''cd armhf
make -j8'''
            
          },
          "build arm64": {
            sh '''cd arm64
make -j8'''
            
          }
        )
      }
    }
    stage('artifacts') {
      steps {
        archiveArtifacts(artifacts: 'parrotsec-*', caseSensitive: true)
      }
    }
  }
}