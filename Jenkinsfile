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
        //publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: 'quality.html', reportName: 'Quality Report', reportTitles: ''])
        sh 'npm --prefix ../workspace@script/coolstore-ui run lint-console'
    }
    
    stage("Unit Test"){
        sh 'echo Unit Testing'
        sh 'npm --prefix ../workspace@script/coolstore-ui run test'
    }
   
    stage("Code Coverage"){
        sh 'echo Code Coverage'
        sh 'npm --prefix ../workspace@script/coolstore-ui run coverage'
   }

   //stage("Dev - Building Application"){
   //     script{
   //         openshift.withCluster() {
   //             openshift.withProject('coolstore-dev-sourabh'){
   //                 openshift.startBuild("web-ui")   
   //             }
   //         }
   //     }
   //}
    
    stage("Functional Testing"){
        //sh 'cd ../workspace@script/coolstore-ui && python functionalTest.py'
        //sh 'pwd'
        //sh 'python functionalTest.py'   
   }
   
   stage("Load Testing"){
         sh 'cd ../workspace@script/coolstore-ui && artillery run perfTest.yml'
         //sh 'artillery run perfTest.yml --output load-test.json && artillery report load-test.json --output load-test-result.html'
   }
   //stage("Dev - Deploying Application"){
   //    openshiftDeploy(deploymentConfig: 'web-ui')
   //}
}
