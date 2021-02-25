pipeline{
    agent {
        docker { image 'ubuntu:18.04' }
    }
    stages{
        stage('Cloning Repository') {
            steps{ 
                script{
                    scmCheckout {
                        clean = true
                    }
                }
            }
        }
        stage('Build'){
            steps{
                // sh 'chmod +x scripts/jenkins/build'
                sh 'scripts/jenkins-pre-build.sh'
                sh 'scripts/jenkins-build.sh'
            }
        }
        stage('Static Code Scan') {
            steps{
                script{
                    staticCodeScan {
                        // generic
                        scanners             = ['protex', 'bdba']
                        scannerType          = ['c','c++']

                        protexProjectName    = 'OpenAMT - RPC'
                        // internal, do not change
                        protexBuildName      = 'rrs-generic-protex-build'
                        
                        protecodeCredentialsId  = 'protecode-scanner-credentials'
                        protecodeGroup          = '25'
                        protecodeScanName       = 'rpc-zip'
                        protecodeDirectory      = './'
                    }
                }
            }
        }
    }
}