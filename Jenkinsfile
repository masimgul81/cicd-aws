node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace') {
        echo 'Cleaning workspace...'
        deleteDir()       
    }

    stage('Clone Repository') {
        echo 'Cloning repository...'
        git(
            branch: 'main',
            url: 'https://github.com/masimgul81/cicd-aws.git',
        )
    }

    stage('Deploy to EC2') {
       echo 'Deploying to EC2...' 
        sh """
            sudo mkdir ${appDir}
            sudo chown -R jenkins:ejenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}
            sudo npm install --production
            sudo npm run build
            sudo fuser -k 3000/tcp || true
            sudo npm run start
        """
    }
}