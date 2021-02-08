pipeline{
    agent any
    def antVersion = 'Ant1.9.4'
    triggers {
        pollSCM('*****')
    }
    parameters {
        string(name: 'GitStartVersion', defaultValue: '', description: 'Start Git Revision for Deployment/Rollback, for Roll back the changes will be Rolled Back to thhis version')

        string(name: 'GitEndVersion', defaultValue: 'HEAD', description: 'End Git Revision for Deployment/Rollback, End Revision Should be Greater Than Start Revision')

        choice(name: 'Build_Type', choices: ['Deploy', 'Validate Only', 'Rollback'], description: '')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
     wrap([$class: 'MaskPasswordsBuildWrapper', varPasswordPairs: [[password: '123ADS', var: 'SF_Password']]]) {
        echo env['SECRET'];
    }
    
   

     wrap([$class: 'MaskPasswordsBuildWrapper', varPasswordPairs: [[password: '123ADS', var: 'SL_Key']]]) {
        echo env['SECRET'];
    }
    properties(
    [
        parameters([choice(choices: 'CISupport/Sandbox/Sandbox_default.properties', description: 'environment to deploy', name: 'property.file.path')]),
        parameters([choice(choices: 'CISupport/Sandbox/taskExecution.properties', description: 'environment to deploy', name: 'execution.property.file')]),
        parameters([choice(choices: '${SF_Password}', description: 'environment to deploy', name: 'sfsb.password')]),
        parameters([choice(choices: '${SL_Key}', description: 'environment to deploy', name: 'souce.labs.access.key')]),
    ]
)
    Stages{
        
        Stage("Build")
        {
            step{
                 withEnv( ["ANT_HOME=${tool antVersion}"] ) {
                 bat '%ANT_HOME%/bin/ant.bat startCICD'
            }
            
        }
        stage("Deploye")
        {
           echo "Deployed ...${SF_Password}"
        }
    }
}
}
