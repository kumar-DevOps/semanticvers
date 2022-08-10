pipeline{
    agent any
   
	stages{
	    stage('branch name') {
		  steps{
			echo "${env.BRANCH_NAME}"
			sh '''
			    gitversion /output buildserver
			'''
            }
        }

		stage('master') {
		    when {
			branch "master"
		    }
		     steps {
			   echo "${env.BRANCH_NAME}"
			   echo "${branch_name}"
			   sh '''
     			     printenv
				  Admi/.dotnet/tools/dontnet-gitversion /output buildserver
               		     '''
			    echo "This is master Branch Executed"
			    script {
					def props = readProperties file: 'gitversion.properties'
					env.GitVersion_SemVer = props.GitVersion_SemVer
					env.GitVersion_FullSemVer = props.GitVersion_FullSemVer
					env.GitVersion_BranchName = props.GitVersion_BranchName
					env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
					env.GitVersion_ = props.GitVersion_MajorMinorPatch
					env.GitVersion_Sha = props.GitVersion_Sha
					echo env.GitVersion_SemVer
					echo env.GitVersion_MajorMinorPatch
					echo env.GitVersion_FullSemver
                }
            }
        }
    }	
}
