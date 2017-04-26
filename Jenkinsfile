
vy

node('node') {


    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){

          checkout scm
       }

       stage('Install Service Metadata into Workspace'){

         sh 'for i in /usr/share/salt-formulas/reclass/service/*; do ln -s $i service/; done'
       }

       stage('Topfile Lint){

            sh '/usr/local/sbin/salt-reclass --top -b .'
       }

       stage('Pillar Lint for node-01'){

         echo 'Lint Pillar for Node-01'
         sh '/usr/local/sbin/salt-reclass --pillar node-01 -b .'

       }

       stage('Cleanup Service Metadata'){

         echo 'Cleanup Service Metadata'
         sh 'rm -rf service'

         mail body: 'project build successful',
                     from: 'jenkins@domain.com',
                     replyTo: 'jenkins@domain.com',
                     subject: 'project build successful',
                     to: 'sebbraun@gmail.com'
       }



    }
    catch (err) {

        currentBuild.result = "FAILURE"

            mail body: "project build error is here: ${env.BUILD_URL}" ,
            from: 'jenkins@domain.com',
            replyTo: 'jenkins@domain.com',
            subject: 'Salt Lint failed',
            to: 'sebbraun@gmail.com'

        throw err
    }

}
