//Shared library invocation
@Library('shared-library@master') _

//Pipeline Syntax starts
pipeline {
   agent any
   environment {
        int BN =  buildnumber1(JFROG_ID)
         JFROG_ID = credentials('jfrogid')
      }
    

   stages {
      stage('Passing Values to Child Job') {
         steps {
		 
    
			script{
				def int intval = "${BN}"
				def newintval = intval - 1
				for (i in 1..newintval) {
				// add your child job below which has to be triggered and pass the parameters	
				build job: "env_test_myjenk", wait: false, parameters: [string(name: 'buildnum', value: "${i}")]
				}                                                                                            
			}
		 }
         
		 
      }
   }
}

def  buildnumber1(String JFROG_ID) {
  String url = "https://jfrgfreetst.jfrog.io/artifactory/api/storage/example-repo-local/?sort"
  int Bnumber = sh(script: "curl -u $JFROG_ID -s $url | grep uri |awk '{print \$3}'| sed 's+\"++g' | sed 's+/++g' | sed 's+,++g' |wc -l",returnStdout: true).trim()
  return Bnumber

}
