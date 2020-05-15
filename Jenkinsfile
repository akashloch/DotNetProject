pipeline {
   agent {label 'master'}
      environment {
         dotnet = 'C:\\Program Files\\dotnet\\sdk\\3.1.202'
      }
      parameters{
         string(name: 'QA_Api_keys', defaultValue: 'oy2a7xcmjwrcefzruzsqpd3zbib6rodeneyr4cfrp6c7ei', description: 'QA Api keys')

      }
      triggers{
         pollSCM('* * * * *')
      }
   stages {
      stage ('Checkout') {
                  steps {
                     git url: 'https://github.com/akashloch/DotNetProject',branch: 'Dev'
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
      stage('Publish') {
         steps {
              bat "dotnet nuget push **\\nupkgs\\*.nupkg -k ${params.QA_Api_keys} -s  https://www.nuget.org/"
            }
         }
      }
}
