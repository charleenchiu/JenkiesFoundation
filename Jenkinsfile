CODE_CHANGES = getGitChanges()
pipline {
    angent any
    stages {
        stage("build") {
            when {
                expression {
                    BRANCH_NAME == 'dev' && CODE_CHANGES == true
                }
            }
            steps {
                echo 'building the application...'
            }
        }

        stage("test") {
            when {
                expression {
                    BRANCH_NAME == 'dev'
                    //使用參數
                    params.executeTests //省略==true
                }
            }
            steps {
                echo 'testing the application...'
            }
        }

        stage("deploy") {
            steps {
                echo 'deploying the application...'
                /*
                // 使用憑證
                // 引用變數一定要用雙引號
                echo "deploying with ${SERVER_CREDENTIALS}"
                sh "${SERVER_CREDENTIALS}"

                withCredentials([
                    usernamePassword(credentials: '', usernameVariable: USER, passwordVariable: PWD)
                ]) {
                    sh "some script ${USER} ${PWD}"
                }
                */

                // 使用參數
                echo "deploying version ${params.VERSION}"
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