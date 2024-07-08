pipeline
{
    agent any
    stages
    {
        stage('contdownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('contbuild')
        {
            steps
            {
               sh 'mvn package' 
            }
        }
        stage('contdeployment')
        {
            steps
            {
             deploy adapters: [tomcat9(credentialsId: '59706b1e-adff-428f-a3cd-3692d07761df', path: '', url: 'http://172.31.50.215:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('conttesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/declarativepipeline/testing.jar'
            }
        }
        stage('contdelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '59706b1e-adff-428f-a3cd-3692d07761df', path: '', url: 'http://172.31.58.111:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
