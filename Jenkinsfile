node('built-in') 
{
    stage('ContinuousDownload')
    {
        git 'https://github.com/intelliqittrainings/maven.git'
    }
    stage('ContinuousBuild')
    {
       sh 'mvn package'
    }
    stage('ContinuousDeployment')
    {
        deploy adapters: [tomcat9(credentialsId: '23987303-7f7e-4cf7-b025-e5942bd46f65', path: '', url: 'http://172.31.85.112:8080')], contextPath: 'testapp', war: '**/*war'
    }
     stage('ContinuousTesting')
    {
       git credentialsId: '23987303-7f7e-4cf7-b025-e5942bd46f65', url: 'https://github.com/intelliqittrainings/FunctionalTesting.git'
       sh 'java -jar /var/lib/jenkins/workspace/ScriptedPipeline/testing.jar'
    }
    stage('ContinuousDelivery')
    {
        input message: 'Need Approval from Oga at the top', submitter: 'harday'
       deploy adapters: [tomcat9(credentialsId: '23987303-7f7e-4cf7-b025-e5942bd46f65', path: '', url: 'http://172.31.91.117:8080')], contextPath: 'prodapp', war: '**/*war'
    }
}