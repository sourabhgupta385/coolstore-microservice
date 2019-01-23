node{
    def NODEJS_HOME = tool "NODE_PATH"
    env.PATH="${env.PATH}:${NODEJS_HOME}/bin"
    sh 'npm --version'
        
    stage('First Time Deployment'){
        script{
            openshift.withCluster() {
                openshift.withProject('coolstore-dev-sourabh') {
                    def bcSelector = openshift.selector( "bc", "web-ui")
                    def bcExists = bcSelector.exists()
                    if (!bcExists) {
                        openshift.newApp("https://raw.githubusercontent.com/sourabhgupta385/coolstore-microservice/stable-ocp-3.9/openshift/coolstore-template.yaml")
                    } else {
                        sh 'echo BC already exists'
                        //openshift.startBuild("web-ui")
                         
                    }
                }
            }
        }
    }
    stage('Install Dependecies'){
        sh 'npm --prefix ../workspace@script/coolstore-ui install'
    }
    stage('Code Quality'){
        sh 'npm --prefix ../workspace@script/coolstore-ui run lint'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: 'quality.html', reportName: 'Quality Report', reportTitles: ''])
        sh 'npm run lint-console'
    }
}
