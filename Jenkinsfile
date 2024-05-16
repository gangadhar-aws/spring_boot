@Library('my-shared-lib') _
pipeline{
    agent any

    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'choose create/destory')
    }

    stages{
        stage('Git Checkout'){
            when { expression { params.action == 'create' } }
            steps{
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/gangadhar-aws/spring_boot.git"
                )
            }
        }

        stage('Maven Unit Test'){
             when { expression { params.action == 'create' } }
            steps{
               mvnTest()
            }
        }

        stage('Integration Test Maven'){
             when { expression { params.action == 'create' } }
            steps{
               mavenIntegration()
            }
        }

        stage('Qode Analaysis Chekcing'){
             when { expression { params.action == 'create' } }
            steps{
                def SonarQubecredentialsId = 'sonarqube-api'
                staticCodeanalysis(SonarQubecredentialsId)

            }
        }





    }
}