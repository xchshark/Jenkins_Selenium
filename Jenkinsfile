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
      curl -l -o dotnet-sdk-6.0.132-win-x86.exe https://download.visualstudio.microsoft.com/download/pr/ad59f1d1-5f19-4474-86be-2f09ab195618/5c7a64445dae84e386bb88e1f6ac09e4/dotnet-sdk-6.0.132-win-x86.exe
      echo installing DotNet SDK 6.0 
      dotnet-sdk-6.0.132-win-x86.exe /quiet /norestart 
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