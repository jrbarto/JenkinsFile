node {
    stage('DEV'){
           checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/jrbarto/Jenkins-Test']]])
           step([$class: 'UCDeployPublisher',
                siteName: 'UCD',
                component: [
                    $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
                    componentName: 'Jenkins',
                    createComponent: [
                        $class: 'com.urbancode.jenkins.plugins.ucdeploy.ComponentHelper$CreateComponentBlock',
                        componentTemplate: '',
                        componentApplication: 'Jenkins-APP'
                    ],
                    delivery: [
                        $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Push',
                        pushVersion: '${BUILD_NUMBER}-Jenkins',
                        baseDir: '/var/jenkins_home/workspace/Pipeline-component_creation',
                        fileIncludePatterns: '*.zip',
                        fileExcludePatterns: '',
                        pushProperties: 'jenkins.server=Local\njenkins.reviewed=true',
                        pushDescription: 'Pushed from Jenkins',
                        pushIncremental: false
                    ]
                ],
                deploy: [
                    $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeployHelper$DeployBlock',
                    deployApp: 'Jenkins-APP',
                    deployEnv: 'Jenkins-ENV',
                    deployProc: 'Deploy Jenkins',
                    createProcess: [
                        $class: 'com.urbancode.jenkins.plugins.ucdeploy.ProcessHelper$CreateProcessBlock',
                        processComponent: 'Wait'
                    ],
                    deployVersions: 'Jenkins:${BUILD_NUMBER}-Jenkins\nJenkins:28-Jenkins',
                    deployOnlyChanged: false
                ]
            ])
    }
}
