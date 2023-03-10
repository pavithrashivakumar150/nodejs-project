def registry = 'https://nodejsapplication.jfrog.io'
def imageName = 'npmimage-docker-local'
def version   = '1.0.2'
pipeline{
    agent {
        node {
            label "valaxy"
        }
    }
    tools {nodejs 'nodejs-16'}

    stages {
        stage('build') {
            steps{
                echo "------------ build started ---------"
               	sh "npm install"
                echo "------------ build completed ---------"
        }
      }

        stage('Unit Test') {
            steps {
                echo '<--------------- Unit Testing started  --------------->'
                sh 'npm test'
                echo '<------------- Unit Testing stopped  --------------->'
            }
        }

stage(" Docker Build ") {
      steps {
        script {
           echo '<--------------- Docker Build Started --------------->'
           app = docker.build(imageName+":"+version)
           echo '<--------------- Docker Build Ends --------------->'
        }
      }
    }

    stage (" Docker Publish "){
        steps {
            script {
               echo '<--------------- Docker Publish Started --------------->'  
                docker.withRegistry(registry, 'jfrog-access'){
                    app.push()
                }    
               echo '<--------------- Docker Publish Ended --------------->'  
            }
        }
    }
            stage('Deployment') {
            steps {
                echo '<--------------- deployment started  --------------->'
                sh './deploy.sh'
                echo '<------------- deployment stopped  --------------->'
            }
        }  
    }
    }
