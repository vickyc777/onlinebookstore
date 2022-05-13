pipeline
{
    agent any
    
    tools
    {
        maven 'Maven3.8.5'
    }
    
        stages
        {
            stage('checkoutCode')
            {
                steps
                {
                    git branch: 'J2EE', credentialsId: 'acf1a30b-30ef-4056-b688-e0077ada08b0', url: 'https://github.com/vickyc777/onlinebookstore.git'
                }
            }
            stage('Build')
            {
                steps
                {
                    sh "mvn clean package"
                }
                    
            }
            stage('ExecuteSonarqubeReport')
            {
                steps
                {
                    sh "mvn sonar:sonar"
                }
            }
            stage('UploadArtifactsIntoNexus')
            {
                steps
                {
                    sh "mvn deploy"
                }
            }
            stage('DeployAppintoTomcat')
            {
                steps
                {
                        sshagent(['38bf683d-742a-45a5-b3cf-7709f745ee43']) 
                     {
                       sh "scp -o StrictHostKeyChecking=no target/onlinebookstore-0.0.1-SNAPSHOT.war ec2-user@3.110.167.246:/opt/apache-tomcat-9.0.62/webapps/"
                     }
                    
}
            
            }
        }
    }
