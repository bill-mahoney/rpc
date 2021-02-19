pipeline{
    agent {
        label 'docker-amt'
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