pipeline{
    agent{
        label 'slave1'
    }
    stages{
        stage('1-clone'){
            steps{
               sh 'cat /etc/passwd'
            }
        }
        stage('2-parallel-jobs'){
            parallel{
                agent{
                    label 'slave2'
                }
                stage('1-subjob1'){
                    steps{
                        sh 'lscpu'
                    }
                }
                stage('2-subjob2'){
                    when{
                        branch 'side'
                    }
                    steps{
                        sh 'df -h'
                    }
                }          
            }
        }
        stage('3-codetest'){
            agent{
                label 'slave1'
            }
            steps{
                sh 'free -m'
            }
        }
        stage('4-clossing'){
            agent{
                label 'slave2'
            }
            steps{
                echo "we are done "
            }
        }
    }
}
