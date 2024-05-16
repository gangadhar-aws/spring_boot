@Library('my-shared-lib') _
pipeline{
    agent any

    stages{
        stage('Git Checkout'){
            steps{
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/gangadhar-aws/spring_boot.git"
                )
            }
        }
    }
}