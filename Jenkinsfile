pipeline {
  agent any
  stages {
    stage('Paso 1: inicio') {
      steps {
        echo 'Entrando a pipeline'
      }
    }
    stage('Paso 2: rama de ejecución') {
      steps {
        echo 'Rama ' + env.BRANCH_NAME
      }
    }
    stage ("Paso 3: Rama de desarrollador") {
      // si no es la rama master entonces ejecuta la integración continua
      when { not { branch 'master' } }
      steps {
        echo "Mensaje"
        withCredentials([usernameColonPassword(credentialsId: '961fd8e1-9d6d-4c89-91a9-1d4269f50160', variable: 'key')]) {
          sh 'git remote set-url origin https://jmelleo:Blankis0926@github.com/jmelleo/Madesoft.git'
          sh 'git fetch origin'
          sh 'git checkout origin/master'
          sh 'git pull . origin/' + "${env.BRANCH_NAME}" + ' --allow-unrelated-histories'
          sh 'git merge origin/' + "${env.BRANCH_NAME}"
          sh 'git push origin HEAD:master'
          echo 'Proceso finalizado exitosamente'
        }
      }
    }
    stage ("Paso 3: Rama master") {
      // si es la rama master no se hace integración
      when { branch 'master'}
      steps {
        echo 'Sólo se ejecuta en ramas de desarrolladores'
      }
    }
  }
}
