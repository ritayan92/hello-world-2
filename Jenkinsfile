pipeline {
    agent any
    
    environment
    {
        PATH="/opt/maven/apache-maven-3.6.3/bin/:$PATH"
    }

    stages {
        stage("git checkout") {
            steps {
                git credentialsId: 'fc9764cb-80d4-4ad2-9ea4-18a001c9fb1c', url: 'https://github.com/ritayan92/hello-world-2'
            }
        }
        stage("build job") {
            steps {
                sh "mvn clean install"
            }
        }
        stage("Deploy war to apache Tomcat") {
            steps {
                sshagent(["${ssh_agent}"]) {
                    sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@${tomcat_ip}:${tomcat_path}"
    // some block
                }
            }
        }
    }
}
