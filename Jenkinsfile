CODE_CHANGES = getGitChanges()
pipline {
    angent any
    //加"環境"變數
    environment {
        NEW_VERSION = '1.3.0'
    }
    //每個CICD的階段
    stages {
        stage("build") {
            //加條件
            when {
                expression {
                    BRANCH_NAME == 'dev' && CODE_CHANGES == true
                }
            }
            steps {
                echo 'building the application...'
                //使用"環境"變數
                echo "building version ${NEW_VERSION}"
            }
        }

        stage("test") {
            when {
                expression {
                    BRANCH_NAME == 'dev'
                }
            }
            steps {
                echo 'testing the application...'
            }
        }

        stage("deploy") {
            steps {
                echo 'deploying the application...'
            }
        }
    }
    post {
        always {
            //deploy後，無論是否成功，一定要做的事
        }
        success {
            //deploy後，若成功要做的事
            echo 'deploy success!'
        }
        failure {
            //deploy後，若失敗要做的事
            echo 'deploy fail!'
        }
    }
}
