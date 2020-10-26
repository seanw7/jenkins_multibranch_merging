pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    environment {
        // setting this for packer, it will use it to get current dir context
        WORKINGDIR = pwd()
        VSPHERE_CREDS = credentials('vsphere_cred')
        ANSIBLE_VAULT_CRED = credentials('ansible_vault_cred')
        TESTVAR = "true"

    }

    stages('Jenkins build') {
        stage('Master branch') {
            when {
                anyOf {
                    branch 'master'
                    branch 'main'
                }
            }
            steps {
                // sh 'echo $USER > test.txt'
                sh 'echo "in master or main branch"'
                sh 'cat testfile.yml'
            }

        }
        stage('Dev branch') {
            when {
                anyOf {
                    branch 'dev'
                    branch 'devel'
                }
            }
            environment {
                BUILD_VERSION = '1.0'  // Important for Morpheus Node Type version number
            }
            steps {
                sh 'echo "in dev, or devel branch"'
                // dir ('ansible'){
                //     sh ''
                // }
                // dir (''){
                //     sh ''
                // }
                // dir (''){
                //     sh '''

                //     '''
                // }

            }
            post {
                success {
                    dir (''){
                        sh '''echo 'build was successful in ${BRANCH_NAME}'''
                    }
                }
                // always {
                //     dir (''){
                //         sh ''
                //     }
                // }
            }
        }

        stage('Feature branch') {
            when {
                not {
                    branch 'master'
                    branch 'main'
                    branch 'dev'
                    branch 'devel'
                }
            }
            environment {
                BUILD_VERSION = '1.0'
            }
            steps {
                // dir ('ansible'){
                    sh 'echo "Not in master, main, dev, or devel branch"'
                // }
            }
            post {
                success {
                    // dir (''){
                        sh '''echo SUCCESS '''
                    // }
                }
            }
        }
    }
}
