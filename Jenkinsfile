pipeline {
  agent any
  stages {
    stage('setup') {
      steps {
        ws(dir: '/home/spf/parrot-builds') {
          sh 'apt-get install live-build qemu-arm-static bootstrap make'
        }
        
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
          "configure aarch64": {
            sh '''cd aarch64
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
          "build aarch64": {
            sh '''cd aarch64
make -j8'''
            
          }
        )
      }
    }
  }
}