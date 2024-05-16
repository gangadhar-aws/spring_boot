@Library('my-shared-lib') _
pipeline{
    agent any

    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'choose create/destory')
        string(name: 'ImageName', description: 'name of the docuer build', defaultvalue: 'javapp')
        string(name: 'ImageTag', description: 'name of the docker build', defaultvalue: 'v1')
        string(name: 'Appname', description: 'name of the Application', defaultvalue: 'springboot')
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

        stage('Static Code analysis: Sonarqube'){
             when { expression { params.action == 'create' } }
            steps{
                script{
                    def SonarQubecredentialsId = 'sonarqube-api'
                    staticCodeanalysis(SonarQubecredentialsId)
                }

            }
        }


        stage('Qulity Gate status check: sonarqube'){
             when { expression { params.action == 'create' } }
            steps{
                script{
                    def SonarQubecredentialsId = 'sonarqube-api'
                    QualityGateStatus(SonarQubecredentialsId)
                }

            }
        }


        stage('Maven Build: maven'){
             when { expression { params.action == 'create' } }
            steps{
                script{
                    mvnBuild()
                }

            }
        }

        //dockerizing the Image
         stage('Docker Image Build'){
             when { expression { params.action == 'create' } }
            steps{
                script{
                    dockerBuild("${params.ImageName}","${params.ImageTag}","${params.Appname}")
                }

            }
        }




            


    }
}