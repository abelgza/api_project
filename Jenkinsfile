//multibranch pipelines
@Library('pipeline-library-demo')_
node {
  checkout scm

  if (env.BRANCH_NAME == 'master') {
    stage ('Inicio Prod') {
      bat label: 'Se inicia en prod', script: 'echo "Se inicia proceso en produccion, puerto 3000"'
    }
    stage ('Se descarga del repo') {
      bat label: 'npm install', script: 'npm install'
    }
    stage ('Deploy') {
      bat label: 'Se inicializa con pm2', script: 'pm2 start server/server.js --name prod_project'
    }
  }

  else if (env.BRANCH_NAME == 'qa') {
    stage ('Inicio QA') {
      bat label: 'Se inicia en QA', script: 'echo "Se inicia proceso en QA, puerto 3200"'
    }
    stage ('Se descarga del repo') {
      bat label: 'npm install', script: 'npm install'
    }
    stage ('Deploy') {
      bat label: 'Se inicializa con pm2', script: 'pm2 start server/server.js --name qa_project'
    }
  }

  else if (env.BRANCH_NAME == 'dev') {

    deployNode(env.BRANCH_NAME, '4100', 'test_nodeProject', 'https://github.com/abelgza/api_project_tester.git')
  }
  else {
    bat label: 'Branch Incorrecto', script: 'echo "No se identifica el branch"'
    bat label: 'Error', script: 'EXIT /B 1'
  }
}
