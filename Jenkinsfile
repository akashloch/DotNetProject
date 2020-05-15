pipeline {
   agent {label 'master'}
      environment {
         dotnet = 'C:\\Program Files\\dotnet\\sdk\\3.1.202'
      }
      parameters{
         string(name: 'Production_Api_keys', default value: 'oy2k2rc4nhmpplqeg3iqnzxedqgac65utgwfqih232wjl4', description: 'Prod Api keys')

      }
      triggers{
         pollSCM('* * * * *')
      }
   stages {
      stage ('Checkout') {
                  steps {
                     git url: 'https://github.com/akashloch/DotNetProject',branch : 'DeployToProd'
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
                  bat "dotnet nuget push **\\nupkgs\\*.nupkg -k ${params.Production_Api_keys} -s https://www.nuget.org/"
            }
         }
         
      }
}
