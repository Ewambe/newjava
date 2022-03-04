pipeline
{
    agent any
    stages
    {
        stage('ContinousDownload')
        {
            steps
            {
            git 'https://github.com/Ewambe/newjava.git'    
            }
        }
        stage('ContinousBuild')
        {
            steps
            {
            sh 'mvn package'    
            }
        }
        stage('ContinousDeployment')
        {
            steps
            {
            deploy adapters: [tomcat9(credentialsId: '24c93484-c125-4361-aa30-fcfe38f0264b', path: '', url: 'http://172.31.5.26:8080')], contextPath: 'testapp', war: '**/*.war'    
            }
        }
        stage('ContinousTesting')
        {
            steps
            {
            git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
            sh 'java -jar /home/ubuntu/.jenkins/workspace/Declarative/testing.jar'
            }
        }
        stage('ContinousDelivery')
        {
            steps
            {
            deploy adapters: [tomcat9(credentialsId: '24c93484-c125-4361-aa30-fcfe38f0264b', path: '', url: 'http://172.31.3.93:8080')], contextPath: 'prodapp', war: '**/*.war'    
            }
        }
    }
}
