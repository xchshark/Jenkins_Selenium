pipeline 
{
agent any
stages
{
   stage('Checkout Code') {
   //checkout the repository
   steps {
      git branch: 'main', url: 'https://github.com/xchshark/Jenkins_Selenium'
   }
   }
   stage('Dotnet Install') {
   //install dotnet
   steps {
      bat '''
      echo Downloading DotNet SDK LelinaTkaPu
      choco install dotnet-sdk -y --version=6.0.100
   
      '''
      }
      }
   stage('Dependecies') {
   //install dependecies
    steps {
      bat 'dotnet restore SeleniumIde.sln'
}
}
   stage('Build') {
  //build
   steps {
      bat 'dotnet restore SeleniumIde.sln --configuration Release'

   }
   }
   stage('Tests') {
   //run tests
   steps {
bat 'dotnet test SeleniumIde.sln --logger"trx;LogFileName=TestResults.trx"'
   }
   }
   
}
post {
   always {
      archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
      step([
         $class: 'MSTestPublisher',
         testResultsFile: '**/TestResults/*.trx'
      ])
   }
}
}