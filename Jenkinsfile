pipeline {
    agent any
      stages {
        stage('Set Environment Variables') {
           steps {
               script {
                   if (env.GIT_BRANCH == 'main') {
                       echo "The git branch is undefined";
                       env.ASTRONOMER_KEY_ID = env.PROD_ASTRONOMER_KEY_ID;
                       env.ASTRONOMER_KEY_SECRET = env.PROD_ASTRONOMER_KEY_SECRET;
                       env.ASTRONOMER_DEPLOYMENT_ID = env.PROD_DEPLOYMENT_ID;
                   } else if (env.GIT_BRANCH == 'dev') {
                       echo "The git branch is undefined";
                       env.ASTRONOMER_KEY_ID = env.DEV_ASTRONOMER_KEY_ID;
                       env.ASTRONOMER_KEY_SECRET = env.DEV_ASTRONOMER_KEY_SECRET;
                       env.ASTRONOMER_DEPLOYMENT_ID = env.DEV_DEPLOYMENT_ID;
                   } else {
                       echo "This git branch undefined is not configured in this pipeline."
                   }
               }
           }
        }
        stage('Deploy to Astronomer') {
          steps {
            script {
              sh 'curl -LJO https://github.com/astronomer/astro-cli/releases/download/v1.4.0/astro_1.4.0_linux_amd64.tar.gz'
              sh 'tar xzf astro_1.4.0_linux_amd64.tar.gz'
              sh "./astro deploy ${ASTRONOMER_DEPLOYMENT_ID} -f"
            }
          }
        }
      }
    post {
      always {
        cleanWs()
      }
    }
   }
}