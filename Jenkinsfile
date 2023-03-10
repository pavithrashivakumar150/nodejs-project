def registry = 'https://nodejsapplication.jfrog.io'
def imageName = 'nodejsapplication.jfrog.io/npmimage-docker-local/demo_nodejs'
def version   = '1.0.2'
pipeline{
    agent {
        node {
            label "nodejs"
        }
    }
    tools {nodejs 'nodejs'}

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
                docker.withRegistry(registry, '	npmjgrog'){
                    app.push()
                }    
               echo '<--------------- Docker Publish Ended --------------->'  
            }
        }
    }
            
    }
    }
