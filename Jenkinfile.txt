pipeline {
    agent none
    stages {
        stage('Non-Parallel stage'){
            agent {
                label "Master"
            }
            steps{
                echo "This stage will be executed first"
            }
        }
        stage("Run Test") {
            parallel {
                stage ("Test on Windows"){
                    agent {
                        label "Windows_Node"
                    }
                    steps {
                        echo "Task1 on Agent"
                    }
                }
                
                stage ("Test on Master") {
                    agent {
                        label "Master"
                    }
                    steps {
                        echo "Task1 on Master"
                    }
                }
            }
        }
    }
}