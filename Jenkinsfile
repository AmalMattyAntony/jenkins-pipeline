pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main' ,url: 'https://github.com/spring-projects/spring-petclinic.git'

                // Run Maven on a Unix agent.
                sh 'mvn package'
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
                node {
                    ansiblePlaybook( 
                        playbook: '/home/vagrant/ansible-jar-playbook.yml',
                        inventory: '/home/vagrant/hosts', 
                        credentialsId: '/var/lib/jenkins/.ssh/id_rsa', 
                }
            }
        }
    }
}
