pipeline {
  agent any
  stages {
    stage('setup') {
      steps {
        ws(dir: '/opt/jenkins/parrot-builds') {
          sh 'apt-get -y install live-build qemu-user-static debootstrap make'
        }
        
        pwd()
      }
    }
    stage('configure armhf') {
      steps {
        parallel(
          "configure armhf": {
            ws(dir: '/opt/jenkins/parrot-builds') {
              sh '''cd armhf
make clean
./configure'''
            }
            
            
          },
          "configure arm64": {
            ws(dir: '/opt/jenkins/parrot-builds') {
              sh '''cd arm64
make clean
./configure'''
            }
            
            
          }
        )
      }
    }
    stage('build armhf') {
      steps {
        parallel(
          "build armhf": {
            ws(dir: '/opt/jenkins/parrot-builds') {
              sh '''cd armhf
make -j8'''
            }
            
            
          },
          "build arm64": {
            ws(dir: '/opt/jenkins/parrot-builds') {
              sh '''cd arm64
make -j8'''
            }
            
            
          }
        )
      }
    }
  }
}