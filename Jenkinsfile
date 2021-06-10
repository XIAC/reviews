pipeline {
  agent any
  stages {
    stage('const') {
      steps {
        echo 'DEMO CONST'
        sh 'sh run_build_script.sh'
      }
    }

    stage('test') {
      parallel {
        stage('test') {
          steps {
            echo 'Ejecutar pruebas de Windows '
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('Windows TEst') {
          steps {
            echo 'Windows Test'
          }
        }

      }
    }

    stage('Deploy staging') {
      steps {
        echo 'Deploy stagin'
        input '¿Aceptar para implementar en producción? '
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploy a produccion'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-team@example.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}