pipeline {
    agent any
    environment {
        PIPELINENAME          = "BenchmarkOWASPParts"
        PIPELINEVERS          = "v1.0201"

        CX_SERVER_URL         = "http://localhost:8080"
        CX_PROJECT_TEAM       = "CxServer\\SP\\Company\\Users"
        CX_PROJECT_NAME       = "BenchmarkOWASPParts"
    }
    parameters {
        string(name: 'CX_USERNAME', defaultValue: 'admin', description: 'Checkmarx Username')
        string(name: 'CX_PASSWORD', defaultValue: 'admin', description: 'Checkmarx Password')
    }    
    stages {
        stage('Git') {
            steps {
                cleanWs() // Workspace Clean Up plugin
                echo "Get some code from an SCM repository..."
                git branch: 'stage_1', url: 'https://github.com/kollol2k/BenchmarkOWASPParts.git'
            }
        }         
        stage('Preparation') {
            steps {
                echo "Get some code from an SCM repository..."
            }
        }
        stage('Checkmarx Security Scan') {
            steps {
                step([$class: 'CxScanBuilder', comment: '', credentialsId: '', excludeFolders: 'sessions,target,webapp', 
                      excludeOpenSourceFolders: '', exclusionsSetting: 'job', failBuildOnNewResults: false, 
                      failBuildOnNewSeverity: 'HIGH', filterPattern: '''!**/_cvs/**/*, !**/.svn/**/*, !**/.txt/**/*,  
                      !**/.hg/**/*,   !**/.git/**/*,  !**/.bzr/**/*, !**/bin/**/*,
                      !**/obj/**/*,  !**/backup/**/*, !**/.idea/**/*, !**/*.DS_Store, !**/*.ipr,     !**/*.iws,
                      !**/*.bak,     !**/*.tmp,       !**/*.aac,      !**/*.aif,      !**/*.iff,     !**/*.m3u, !**/*.mid, !**/*.mp3,
                      !**/*.mpa,     !**/*.ra,        !**/*.wav,      !**/*.wma,      !**/*.3g2,     !**/*.3gp, !**/*.asf, !**/*.asx,
                      !**/*.avi,     !**/*.flv,       !**/*.mov,      !**/*.mp4,      !**/*.mpg,     !**/*.rm,  !**/*.swf, !**/*.vob,
                      !**/*.wmv,     !**/*.bmp,       !**/*.gif,      !**/*.jpg,      !**/*.png,     !**/*.psd, !**/*.tif, !**/*.swf,
                      !**/*.jar,     !**/*.zip,       !**/*.rar,      !**/*.exe,      !**/*.dll,     !**/*.pdb, !**/*.7z,  !**/*.gz,
                      !**/*.tar.gz,  !**/*.tar,       !**/*.gz,       !**/*.ahtm,     !**/*.ahtml,   !**/*.fhtml, !**/*.hdm,
                      !**/*.hdml,    !**/*.hsql,      !**/*.ht,       !**/*.hta,      !**/*.htc,     !**/*.htd, !**/*.war, !**/*.ear,
                      !**/*.htmls,   !**/*.ihtml,     !**/*.mht,      !**/*.mhtm,     !**/*.mhtml,   !**/*.ssi, !**/*.stm,
                      !**/*.stml,    !**/*.ttml,      !**/*.txn,      !**/*.xhtm,     !**/*.xhtml,   !**/*.class, !**/*.iml, 
                      !Checkmarx/Reports/*.*''', fullScanCycle: 10, //groupId: '69c7e3b5-3b66-4558-bc03-c14e2f2c7173', 
                      includeOpenSourceFolders: '', osaArchiveIncludePatterns: '*.zip, *.war, *.ear, *.tgz', osaInstallBeforeScan: false, 
                      preset: '36', teamPath: "${CX_PROJECT_TEAM}", projectName: "${CX_PROJECT_NAME}", sastEnabled: true, serverUrl: "${CX_SERVER_URL}", 
                      sourceEncoding: '1', username: "${params.CX_USERNAME}", password: "${params.CX_PASSWORD}", 
                      vulnerabilityThresholdResult: 'FAILURE', waitForResultsEnabled: true, generatePdfReport: true])
 
            }
        }
    }
    post {
        always {
            echo "${PIPELINENAME} (${PIPELINEVERS}) - Build ${BUILD_NUMBER} is done..."
        }
    }
}
