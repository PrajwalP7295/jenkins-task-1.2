pipeline { 
  
   agent any

   stages {
   
     stage('Install Dependencies') { 
        steps { 
           sh 'npm install' 
        }
     }
     
     stage('Test Application') { 
        steps { 
           sh 'echo "testing application..."'
        }
      }

         stage("Deploy application") { 
         steps { 
           sh 'echo "deploying application..."'
         }

     }
     
     stage('Build Docker Image') {
        steps {
            script {
                sh 'docker build -t prajwalp7295/mynodejsapp-1.0 .'
            }
        }
     }
     
     stage("Push Docker image") {
        steps {
            script {
		    withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerhubpwd')]) {
                    sh "docker login -u prajwalp7295 -p ${dockerhubpwd}"
                }
                sh "docker push prajwalp7295/mynodejsapp-1.0"
            }
        }
     }
      stage('Run Docker Container') {
        steps {
            sh 'docker run -d --name mynodejsapp -p 8888:8888 prajwalp7295/mynodejsapp-1.0'
        }
     }
  
   }
}
