pipeline {
agent any

stages {
stage ('Git') {
   steps {
       git 'https://github.com/krish3402/react-112.git'
    }
}
stage('Front End') {
    steps {
    println 'Front End Start'
    }
  }
stage ('Node & npm Install') {
    steps {
        sh label: '', script: 'sudo apt-get install nodejs -y' 
        sh label: '', script: 'sudo apt-get install npm -y'
        
    }
}
stage ('version') {
    steps {
        sh label: '', script: 'node -v'
        sh label: '', script: 'npm -v'
    }
}
stage ('npm packages install') {
    steps {
        sh label: '', script: 'cd client && npm install && npm i -D jest-junit-reporter'
    }
}
stage ('npm Coverage & Test Result') {
    steps {
        sh label: '', script: 'cd client && npm test -- --coverage --watchAll=false'
    }
}
stage ('Front End Coverage report') {
    steps {
        cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'client/coverage/cobertura-coverage.xml ', conditionalCoverageTargets: '70, 0, 0', enableNewApi: true, failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
       
    }
}
stage ("Front End Test Report") {
steps {

xunit([JUnit(deleteOutputFiles: true, failIfNotNew: true, pattern: 'client/*.xml', skipNoTestFiles: false, stopProcessingIfError: true)])
}
}
stage("Back End") {
    steps {
    println 'Back End Start'
    }
  }

stage ("Maven Install") {
steps {

sh label: '', script: 'sudo apt-get install maven -y'
}
}
stage ("Maven build") {
steps {

sh label: '', script: 'mvn clean install cobertura:cobertura'
}
}
stage ("Back End Coverage Report") {
steps {

cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml	', conditionalCoverageTargets: '70, 0, 0', enableNewApi: true, failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
}
}
stage ("Back End Test Report") {
steps {

xunit([JUnit(deleteOutputFiles: true, failIfNotNew: true, pattern: '**/surefire-reports/*.xml', skipNoTestFiles: false, stopProcessingIfError: true)])
}
}
}
}

