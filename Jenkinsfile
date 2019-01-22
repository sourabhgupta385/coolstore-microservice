pipeline{
    agent none
    stages{
        stage('First Time Deployment'){
            steps{
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
                                sh 'cd coolstore-ui'
                                sh 'ls'
                            }
                        }
                    }
                }
            }
        }
        
    }
}
