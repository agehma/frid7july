pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/agehma/frid7july.git'
                    }
                    catch (Exception e1)
                    {
                        mail bcc: '', body: 'git failed to download the code from github repository', cc: '', from: '', replyTo: '', subject: 'first download failed ', to: 'gt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch (Exception e2)
                    {
                        mail bcc: '', body: 'mvn failed to build an artifact for the new project', cc: '', from: '', replyTo: '', subject: 'mvn failed to build', to: 'dvt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.91.123:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch (Exception e3)
                    {
                        mail bcc: '', body: 'unable to deploy artifact into tomcat of qaserver', cc: '', from: '', replyTo: '', subject: 'tomcat failed to deploy', to: 'mwt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                       git 'https://github.com/agehma/testingscript1.git'
                       sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipelinePE1/testing.jar'
                    }
                    catch (Exception e4)
                    {
                        mail bcc: '', body: 'selenium failed to test artifact from qaserver', cc: '', from: '', replyTo: '', subject: 'selenium failed', to: 'st@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.85.56:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch (Exception e5)
                    {
                        mail bcc: '', body: 'unable to deliver into prodserver at this time', cc: '', from: '', replyTo: '', subject: 'delivery failed', to: 'dt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
    }
}

