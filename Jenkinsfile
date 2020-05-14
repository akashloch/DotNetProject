pipeline {
agent {label 'master'}
environment {
dotnet = 'C:\\Program Files\\dotnet\\sdk\\3.1.202'
}
stages {
stage ('Checkout') {
            steps {
                 git credentialsId: 'akashloch', url: 'https://github.com/akashloch/DotNetProject',branch: 'master'
            }
}
stage ('Restore PACKAGES') {     
         steps {
             bat "dotnet restore"
          }
        }
stage('Clean') {
      steps {
            bat 'dotnet clean'
       }
    }
stage('Build') {
     steps {
            bat 'dotnet build --configuration Release'
      }
   }
stage('Pack') {
     steps {
           bat 'dotnet pack --no-build --output nupkgs'
      }
   }
}
}
