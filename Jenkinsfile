pipeline{
    agent none
    stages{
        stage('First Time Deployment'){
            steps{
                script{
                    openshift.withCluster() {
                        openshift.withProject('coolstore-dev') {
                            def bcSelector = openshift.selector( "bc", "web-ui")
                            def bcExists = bcSelector.exists()
                            if (!bcExists) {
                                openshift.newApp("https://raw.githubusercontent.com/sourabhgupta385/coolstore-microservice/stable-ocp-3.9/openshift/coolstore-template.yaml")
                            } else {
                                sh 'echo BC already exists'
                                //openshiftBuild(buildConfig: 'web-ui',showBuildLogs: 'true', namespace: 'coolstore-dev')
                                //sh 'oc start-build web-ui --follow -n coolstore-dev'
                                openshift.startBuild("web-ui")
                                //openshift.startBuild("https://raw.githubusercontent.com/sourabhgupta385/coolstore-microservice/stable-ocp-3.9/openshift/coolstore-template.yaml")
                            }
                        }
                    }
                }
            }
        }
        
    }
}
