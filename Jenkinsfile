/*
 * This file will get basics details of jobs like service-name, pipeline job name ad branch
 * it will also checkout the scm code for that branch if the job is not deploy only job
 */

def call(script) 
{
	try
        {
                wrap([$class: 'AnsiColorBuildWrapper']) {
			def dateStamp = sh(returnStdout: true, script: "echo ${BUILD_TIMESTAMP} | cut -f1 -d' '").trim()
			def hourStamp = sh(returnStdout: true, script: "echo ${BUILD_TIMESTAMP} | cut -f2 -d' ' | cut -f1,2 -d':'").trim()
			hourStamp = hourStamp.replaceAll(':','-')
			timeStamp = "${dateStamp}-${hourStamp}"
			env.TIMESTAMP = timeStamp
			
			sh("cp /home/jenkins/.netrc /root/")
			sh("cp /home/jenkins/.gitconfig /root/")
			sh("cp -rfp /home/jenkins/.ssh /root/")
			sh("chown root:root /root/.ssh/config")

			def jobObj = new com.ftd.workflow.JobManager(script)
			def pipeline = jobObj.getPipelineName()

		        if( ! pipeline.contains("test"))
		        {
				stage('SCM Checkout')
				{
					println "\u001B[32m[INFO] Check out SCM"
					checkout(scm)
				}
			}
		}
		currentBuild.result = "SUCCESS"
	}
	catch (err) {
        	wrap([$class: 'AnsiColorBuildWrapper']) {	
                	println "\u001B[31m[ERROR]: Failed at Fetching Job Details or Checkout SCM"
                        currentBuild.result = "FAILED"
			EmailNotifications(this)
                        throw err
                 }
        }
}



