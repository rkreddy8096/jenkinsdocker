pipeline {
    agent { label "jdk-11" }
    triggers { pollSCM('* * * * *') }
    stages {
        stage ('clone') {
            steps {
                git branch: 'master', url: "https://github.com/DevProjectsForDevOps/StudentCoursesRestAPI.git"
            }
        }

        stage ('imagebuild')  {
            steps {
                sh "curl -fsSL https://get.docker.com -o get-docker.sh"
                sh "sh get-docker.sh"
                sh 'sudo chmod 666 /var/run/docker.sock'
                sh 'sudo usermod -aG docker ubuntu'     
                sh 'sudo systemctl restart docker'
                sh "docker image build -t studentapi:1.0 ."
                sh "docker image tag studentapi:1.0 reddy8096/studentapi:1.0"
                sh "docker image push reddy8096/studentapi:1.0"
            }
        }

        stage ('deploy') {
            steps {
                sh "docker container run -d -P studentapi:1.0"
            }
        }

    }    
}

    }    
}
