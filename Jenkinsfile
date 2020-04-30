node{
    stage('SCM checkout'){
       git credentialsId: 'git', url: 'https://github.com/traorea4/simple_api.git'
    }
    stage('download student_age.json'){
        sshPublisher(publishers: [sshPublisherDesc(configName: 'dev1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'cd /root/pozos', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//root//pozos', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'student_age.json')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
    }
    stage('download project'){
        sshPublisher(publishers: [sshPublisherDesc(configName: 'dev1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'cd /opt/students', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//root//pozos', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'student_age.py')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false), sshPublisherDesc(configName: 'dev1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /root/pozos
##docker login --username "root" --password "centos" docker.io
docker build -t student_age .
docker tag student_age 192.168.128.137:5000/root/student_age:v1 
docker push 192.168.128.137:5000/root/student_age:v1
docker rmi student_age  registry:5000/root/student_age:v1
cd /root/pozos/simple_api
ansible-playbook student_age_playbook.yml --user=centos --extra-vars "ansible_sudo_pass=centos"
''', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//root//pozos//simple_api', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'Dockerfile')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
    }
}
