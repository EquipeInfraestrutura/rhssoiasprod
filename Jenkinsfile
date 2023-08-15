pipeline {
    agent any

    stages {

        stage('Checkout source') {
            steps {
                git url: 'https://github.com/EquipeInfraestrutura/rhssoiasprod.git', branch: 'main'
            }
        }

        stage('Criação ou atualização da infra RHSSO_PROD') {
            environment {
                bucket = credentials('bucket')
                key = credentials('key_rhssoprod')
                region = credentials('region')
                AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
                AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
                AWS_REGION = credentials ('AWS_REGION')

            }
            steps {
                
                script {
                    dir('src') {
                        sh 'terraform init -migrate-state --backend-config "bucket=${bucket}" --backend-config "key=${key}" --backend-config "region=${region}"'
                        sh 'terraform validate'
                        sh 'terraform apply --auto-approve'
                    }
                }
            }
        }

    }

}
