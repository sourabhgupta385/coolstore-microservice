pipeline{
    agent none
    stages{
        stage('First Time Deployment'){
            steps{
                script{
                    openshift.withCluster() {
                        openshift.withProject('coolstore-dev') {
                            def templateSelector = openshift.selector( "template", "coolstore")
                            def templateExists = templateSelector.exists()
                            if (!templateExists) {
                                template = openshift.create('https://raw.githubusercontent.com/sourabhgupta385/coolstore-microservice/stable-ocp-3.9/openshift/coolstore-template.yaml')
                                openshift.process(template)
                            } else {
                                sh 'echo Template already exists'
                            }
                        }
                        openshift.withProject('coolstore-test') {
                            def templateSelector = openshift.selector( "template", "coolstore")
                            def templateExists = templateSelector.exists()
                            if (!templateExists) {
                                template = openshift.create('https://raw.githubusercontent.com/sourabhgupta385/coolstore-microservice/stable-ocp-3.9/openshift/coolstore-template.yaml')
                                openshift.process(template)
                            } else {
                                sh 'echo Template already exists'
                            }
                        }
                        openshift.withProject('coolstore-prod') {
                            def templateSelector = openshift.selector( "template", "coolstore")
                            def templateExists = templateSelector.exists()
                            if (!templateExists) {
                                template = openshift.create('https://raw.githubusercontent.com/sourabhgupta385/coolstore-microservice/stable-ocp-3.9/openshift/coolstore-template.yaml')
                                openshift.process(template)
                            } else {
                                sh 'echo Template already exists'
                            }
                        }
                    }
                }
            }
        }
        
    }
}
