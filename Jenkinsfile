node('master') {
    stage('ContinuousDownload') 
    {
   git 'https://github.com/sunnyk0706/july-maven-repo.git'
    }
    stage('ContinuousBuild')
    {

	sh label: '', script: 'mvn -f  /home/ubuntu/.jenkins/workspace/PipelineAsCode/ScriptedPipelineNewGit/maven/pom.xml package'
        archiveArtifacts '**/*.war'
    }
    stage('ContinuousDeployment')
    {
        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/PipelineAsCode/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.88.35:/var/lib/tomcat8/webapps/testingapp.war'
        
    }
    
}
node('slave1')
{
    stage('ContinuousTesting')
    {
        git 'https://github.com/sunnyk0706/FunctionalTesting.git'
        sh label: '', script: 'java -jar /home/ubuntu/slave_ws/workspace/PipelineAsCode/ScriptedPipeline/testing.jar'
    }
}
node('master')
{
    stage('ContinousDelivery')
    {
        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/PipelineAsCode/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.94.229:/var/lib/tomcat8/webapps/productionapp.war'
    }
}
