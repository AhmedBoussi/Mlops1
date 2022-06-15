 pipeline {
 
 agent any
     
    stages {
        stage('Getting Project from Git') {
            steps {
                echo 'Project is downloading...'
                git branch:'master', url:'https://github.com/AhmedBoussi/Mlops1.git'
  
                 }
             }
          stage('Building docker container') {
            steps {
                script {
                  sh 'docker build -t adult-model .'
                  sh 'docker run -d --name model adult-model'
                   }
               }
           }
            stage('Preprocessing stage') {
            steps {
                script {
                   sh 'docker container exec model python3 preprocessing.py'
 		            	}
               }
           }
           stage('Training stage') {
            steps {
                script {
                    sh 'docker container exec model python3 train.py'
 	            	  	}
                }
        }
        stage('Test stage') {
              steps {
                script {
                    sh 'docker container exec model python3 train.py'
                    sh 'docker container exec model python3 test.py'
                    sh 'docker container exec model cat /home/jovyan/results/train_metadata.json /home/jovyan/results/test_metadata.json' 
                    sh 'docker rm -f model'
 			                 }
                  }
               }
    }
}
