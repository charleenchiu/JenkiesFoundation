CODE_CHANGES = getGitChanges()
pipline {
    angent any
    // build tools
    tools {
        //maven 'Maven'
        //gradle
        //jdk
    }
    //加"環境"變數
    environment {
        NEW_VERSION = '1.3.0'
        //加憑證
        SERVER_CREDENTIALS = credentials('d108c9d8-ee58-4628-9d45-7664a50a20b9')
        //my-app: d108c9d8-ee58-4628-9d45-7664a50a20b9
        //system: cbb5c283-2b83-46be-a71f-8e64d2366a70
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
                // 引用變數一定要用雙引號
                // 使用憑證
                echo "deploying with ${SERVER_CREDENTIALS}"
                sh "${SERVER_CREDENTIALS}"

                withCredentials([
                    usernamePassword(credentials: '', usernameVariable: USER, passwordVariable: PWD)
                ]) {
                    sh "some script ${USER} ${PWD}"
                }
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
