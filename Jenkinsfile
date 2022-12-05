pipeline {
  agent {
    node {
      label 'workstation'
    }
  }

  parameters {
    choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Pick Env')
    choice(name: 'COMPONENT', choices: ['frontend', 'catalogue', 'mongodb'], description: 'Pick Component')
  }

  environment {
    SSH = credentials('SSH')
  }

  stages {

    stage('Clone Ansible Repo') {
      steps {
        git branch: 'main', url: 'https://github.com/bjreddy009037/roboshop-ansible.git'
      }
    }

    stage('Create EC2 Server') {
      steps {
        sh 'bash create-ec2-with-env.sh ${COMPONENT} ${ENV}'
      }
    }

    stage('Run Ansible') {
      steps {
        sh 'ansible-playbook -i inv roboshop.yml -e HOST=${COMPONENT} -e ROLE_NAME=${COMPONENT} -e ENV=${ENV} -e ansible_user=${SSH_USR} -e ansible_password=${SSH_PSW}'
      }
    }

  }

}