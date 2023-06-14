pipeline {
    agent { label 'ansible_jenkins' }
    stages {
        stage('clone sources') {
            steps {
                git branch: 'main',
                url: 'https://github.com/manohargatla/spring-petclinic.git' 
            }
        }
        stage('build package') {
            steps {
                sh 'cd ${WORKSPACE} && ./mvnw package'
            }
        }/*
        stage('copy build package') {
            steps {
                sh 'sudo cp ${WORKSPACE}/target/spring-petclinic-3.0.0-SNAPSHOT.jar /home/spring/spring-petclinic'
            }
        }*/
        stage('apply playbook') {
            steps {
                sh 'ansible -i hosts -m ping all'
                sh 'ansible-playbook -i hosts spring-petclinic.yaml'
            }
        }
        
    }
}