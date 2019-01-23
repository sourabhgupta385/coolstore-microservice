node{
    def NODEJS_HOME = tool "NODE_PATH"
    env.PATH="${env.PATH}:${NODEJS_HOME}/bin"
    sh 'npm --version'
    //agent none
    //stages{
        stage('First Time Deployment'){
            //steps{
                script{
                    openshift.withCluster() {
                        openshift.withProject('coolstore-dev-sourabh') {
                            def bcSelector = openshift.selector( "bc", "web-ui")
                            def bcExists = bcSelector.exists()
                            if (!bcExists) {
                                openshift.newApp("https://raw.githubusercontent.com/sourabhgupta385/coolstore-microservice/stable-ocp-3.9/openshift/coolstore-template.yaml")
                            } else {
                                sh 'echo BC already exists'
                                openshift.startBuild("web-ui")
                                sh 'npm --prefix ../workspace@script/coolstore-ui install' 
                            }
                        }
                    }
                }
            //}
        }
        
   // }
}
