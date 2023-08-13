pipeline
{
    agent any
    stages
    {
        stage('Continoud Download')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('Continous Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Continous Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'b06da7ad-d66e-4792-819c-85d682f068a0', path: '', url: 'http://172.31.40.202:8080')], contextPath: 'testapp1', war: '**/*.war'
            }
        }
        stage('Continous Testing')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('Continous Delivery')
        {
            steps
            {
                input message: 'Need to approval for DM', submitter: 'gayatri'
                
                deploy adapters: [tomcat9(credentialsId: 'b06da7ad-d66e-4792-819c-85d682f068a0', path: '', url: 'http://172.31.37.177:8080')], contextPath: 'prodapp1', war: '**/*.war'
            }
        }
    }
}
