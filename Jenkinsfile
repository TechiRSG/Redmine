pipeline {
agent any
stages {
    stage('checkout') {
                steps {
                        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/suryatejayalla/Redmine']]])
                    }
}
stage('Prerequisite for deployment K8s') {
                steps {
                        sh 'if [ -d "/opt/ans-dep" ]; then rm -r /opt/ans-dep; fi'
                        sh 'mkdir /opt/ans-dep'
                        sh 'cp -r $WORKSPACE/ /opt/ans-dep'
                        sh 'sleep 10s'
                    }
}
stage('setting up deployment K8s') {
                steps {
                        sh 'ansible-playbook -i /$WORKSPACE/hosts redmine-playbook.yml'
                    }
}
stage('post deployment cleanup') {
                steps {
                        sh 'rm -r /$WORKSPACE/*'
                    }
}
}
}
