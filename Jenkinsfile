def NODE_NAME = 'AWS_Instance_CentOS'
def BRANCH_NAME = 'Branch [' + env.BRANCH_NAME + ']'
def BUILD_INFO = 'Jenkins job: ' + env.BUILD_URL
def MAIL_TO='minh.leanh@toshiba-tsdv.com'
def MAIL_SUBJECT='[CI PGSpider] SQLite FDW Test FAILED ' + BRANCH_NAME
def SQLITE_FDW_URL = 'https://github.com/MinhLA1410/sqlite_fdw.git'

def retrySh(String shCmd) {
    def MAX_RETRY = 10
    script {
        int status = 1;
        for (int i = 0; i < MAX_RETRY; i++) {
            status = sh(returnStatus: true, script: shCmd)
            if (status == 0) {
                echo "SUCCESS: "+shCmd
                break
            } else {
                echo "RETRY: "+shCmd 
                sleep 5
            }
        }
        if (status != 0) {
            sh(shCmd)
        }
    }
}

pipeline {
    agent {
        node {
            label NODE_NAME
        }
    }
    triggers {
        pollSCM('H/30 * * * *')
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                    rm -rf postgresql || true
                    tar -zxvf /home/jenkins/Postgres/postgresql.tar.gz > /dev/null
                '''
                dir("postgresql/contrib") {
                    sh 'rm -rf sqlite_fdw || true'
                    retrySh('git clone ' + SQLITE_FDW_URL)
                }
            }
            post {
                failure {
                    echo '** BUILD FAILED !!! NEXT STAGE WILL BE SKIPPED **'
                    emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${BUILD_LOG, maxLines=200, escapeHtml=false}', to: "${MAIL_TO}", attachLog: false
                }
            }
        }
        stage('sqlite_fdw_test') {
            steps {
                dir("postgresql/contrib/sqlite_fdw") { 
                    catchError() {
                        sh '''
                            chmod +x ./*.sh || true
                            rm -rf make_check.out || true
                            ./test_extra.sh
                        '''
                    }
                    script {
                        status = sh(returnStatus: true, script: "grep -q 'All [0-9]* tests passed' 'make_check.out'")
                        if (status != 0) {
                            unstable(message: "Set UNSTABLE result")
                            emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${FILE,path="make_check.out"}', to: "${MAIL_TO}", attachLog: false
                            sh 'cat regression.diffs || true'
                        }
                    }
                }
            }
        }
        stage('Build 9.6.18') {
            steps {
                sh '''
                    rm -rf postgresql || true
                    tar -zxvf /home/jenkins/Postgres/postgresql-9.6.18.tar.gz > /dev/null
                '''
                dir("postgresql/contrib") {
                    sh 'rm -rf sqlite_fdw || true'
                    retrySh('git clone ' + SQLITE_FDW_URL)
                }
            }
            post {
                failure {
                    echo '** BUILD FAILED !!! NEXT STAGE WILL BE SKIPPED **'
                    emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${BUILD_LOG, maxLines=200, escapeHtml=false}', to: "${MAIL_TO}", attachLog: false
                }
            }
        }
        stage('sqlite_fdw_test 9.6.18') {
            steps {
                dir("postgresql/contrib/sqlite_fdw") { 
                    catchError() {
                        sh '''
                            chmod +x ./*.sh || true
                            rm -rf make_check.out || true
                            ./test_extra.sh
                        '''
                    }
                    script {
                        status = sh(returnStatus: true, script: "grep -q 'All [0-9]* tests passed' 'make_check.out'")
                        if (status != 0) {
                            unstable(message: "Set UNSTABLE result")
                            emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${FILE,path="make_check.out"}', to: "${MAIL_TO}", attachLog: false
                            sh 'cat regression.diffs || true'
                        }
                    }
                }
            }
        }
        stage('Build 10.13') {
            steps {
                sh '''
                    rm -rf postgresql || true
                    tar -zxvf /home/jenkins/Postgres/postgresql-10.13.tar.gz > /dev/null
                '''
                dir("postgresql/contrib") {
                    sh 'rm -rf sqlite_fdw || true'
                    retrySh('git clone ' + SQLITE_FDW_URL)
                }
            }
            post {
                failure {
                    echo '** BUILD FAILED !!! NEXT STAGE WILL BE SKIPPED **'
                    emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${BUILD_LOG, maxLines=200, escapeHtml=false}', to: "${MAIL_TO}", attachLog: false
                }
            }
        }
        stage('sqlite_fdw_test 10.13') {
            steps {
                dir("postgresql/contrib/sqlite_fdw") { 
                    catchError() {
                        sh '''
                            chmod +x ./*.sh || true
                            rm -rf make_check.out || true
                            ./test_extra.sh
                        '''
                    }
                    script {
                        status = sh(returnStatus: true, script: "grep -q 'All [0-9]* tests passed' 'make_check.out'")
                        if (status != 0) {
                            unstable(message: "Set UNSTABLE result")
                            emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${FILE,path="make_check.out"}', to: "${MAIL_TO}", attachLog: false
                            sh 'cat regression.diffs || true'
                        }
                    }
                }
            }
        }
        stage('Build 11.8') {
            steps {
                sh '''
                    rm -rf postgresql || true
                    tar -zxvf /home/jenkins/Postgres/postgresql-11.8.tar.gz > /dev/null
                '''
                dir("postgresql/contrib") {
                    sh 'rm -rf sqlite_fdw || true'
                    retrySh('git clone ' + SQLITE_FDW_URL)
                }
            }
            post {
                failure {
                    echo '** BUILD FAILED !!! NEXT STAGE WILL BE SKIPPED **'
                    emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${BUILD_LOG, maxLines=200, escapeHtml=false}', to: "${MAIL_TO}", attachLog: false
                }
            }
        }
        stage('sqlite_fdw_test 11.8') {
            steps {
                dir("postgresql/contrib/sqlite_fdw") { 
                    catchError() {
                        sh '''
                            chmod +x ./*.sh || true
                            rm -rf make_check.out || true
                            ./test_extra.sh
                        '''
                    }
                    script {
                        status = sh(returnStatus: true, script: "grep -q 'All [0-9]* tests passed' 'make_check.out'")
                        if (status != 0) {
                            unstable(message: "Set UNSTABLE result")
                            emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${FILE,path="make_check.out"}', to: "${MAIL_TO}", attachLog: false
                            sh 'cat regression.diffs || true'
                        }
                    }
                }
            }
        }
        stage('Build 12.3') {
            steps {
                sh '''
                    rm -rf postgresql || true
                    tar -zxvf /home/jenkins/Postgres/postgresql-12.3.tar.gz > /dev/null
                '''
                dir("postgresql/contrib") {
                    sh 'rm -rf sqlite_fdw || true'
                    retrySh('git clone ' + SQLITE_FDW_URL)
                }
            }
            post {
                failure {
                    echo '** BUILD FAILED !!! NEXT STAGE WILL BE SKIPPED **'
                    emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${BUILD_LOG, maxLines=200, escapeHtml=false}', to: "${MAIL_TO}", attachLog: false
                }
            }
        }
        stage('sqlite_fdw_test 12.3') {
            steps {
                dir("postgresql/contrib/sqlite_fdw") { 
                    catchError() {
                        sh '''
                            chmod +x ./*.sh || true
                            rm -rf make_check.out || true
                            ./test_extra.sh
                        '''
                    }
                    script {
                        status = sh(returnStatus: true, script: "grep -q 'All [0-9]* tests passed' 'make_check.out'")
                        if (status != 0) {
                            unstable(message: "Set UNSTABLE result")
                            emailext subject: "${MAIL_SUBJECT}", body: BUILD_INFO + "\nGit commit: " + env.GIT_URL.replace(".git", "/commit/") + env.GIT_COMMIT + "\n" + '${FILE,path="make_check.out"}', to: "${MAIL_TO}", attachLog: false
                            sh 'cat regression.diffs || true'
                        }
                    }
                }
            }
        }
    }
}