@Library('shared-library@master') _

//Pipeline Syntax starts
pipeline {
   agent any
   environment {
      int BN =  '4'
		//buildnumber1(JFROG_ID)
         JFROG_ID = credentials('jfrogid')
    url = "https://jfrgfreetst.jfrog.io/artifactory/api/storage/example-repo-local"
	   url_new = "https://jfrgfreetst.jfrog.io/artifactory/api/storage/example-repo-local/?sort"
    //folder_path = curlmethod(url,JFROG_ID,BN)
    //Path = "${url}/${folder_path}/?sort"
   image_name = curlmethodnew(Path, JFROG_ID)
      
      }
    

   stages {
      stage('Passing Values to Child Job') {
         steps {
		 
    
			script{
				def int intval = sh(script: "curl -u $JFROG_ID -s $url_new | grep uri |awk '{print \$3}'| sed 's+\"++g' | sed 's+/++g' | sed 's+,++g' |sed 's+'https:jfrgfreetst.jfrog.ioartifactoryapistorageexample-repo-local'++g' | sed 's+'Mypath2'++' | sort -u -r | head -c -1 |wc -l",returnStdout: true).trim()
				echo "$intval"
				//def newintval = intval - 1
				for (i in 1..4) {
				// add your child job below which has to be triggered and pass the parameters	
					//xz = "${i}"
					def folder_path = curlmethod(url,JFROG_ID,i)
					def Path = "${url}/${folder_path}/?sort"
					def SN = curlmethod(url_new,JFROG_ID,i)
					def RL = curlmethodnew(Path, JFROG_ID)
				build job: "env_test_myjenk", wait: false, parameters: [
					string(name: 'SERVICE_NAME', value : 'SN'),
					string(name: 'RELEASE_LABEL', value : 'RL' )
				  ]
				
				}                                                                                            
			}
		 }
         
		 
      }
   }
}

def  buildnumber1(String JFROG_ID) {
  String url = "https://jfrgfreetst.jfrog.io/artifactory/api/storage/example-repo-local/?sort"
  int Bnumber = sh(script: "curl -u $JFROG_ID -s $url | grep uri |awk '{print \$3}'| sed 's+\"++g' | sed 's+/++g' | sed 's+,++g' |sed 's+'https:jfrgfreetst.jfrog.ioartifactoryapistorageexample-repo-local'++g' | sed 's+'Mypath2'++' | sort -u -r | head -c -1 |wc -l",returnStdout: true).trim()
  return Bnumber

}

def curlmethod(String url, String JFROG_ID,int bn ) {

 String lt
    if(bn > 1){
        lt = sh(script: "curl -u $JFROG_ID -s $url | grep uri |awk '{print \$3}'| sed 's+\"++g' | sed 's+/++g' | sed 's+,++g' |sed 's+'https:jfrgfreetst.jfrog.ioartifactoryapistorageexample-repo-local'++g' | sed 's+'Mypath2'++' | sort -u -r | head -c -1 | head -$bn | tail -1", returnStdout: true).trim();
    }else{
        lt = sh(script: "curl -u $JFROG_ID -s $url | grep uri |awk '{print \$3}'| sed 's+\"++g' | sed 's+/++g' | sed 's+,++g' |sed 's+'https:jfrgfreetst.jfrog.ioartifactoryapistorageexample-repo-local'++g' | sed 's+'Mypath2'++' | sort -u -r | head -c -1 | head -$bn", returnStdout: true).trim();
    }
    
    return lt

}
def curlmethodnew(String Path, String JFROG_ID ) {

String resp = sh(script: "curl -u $JFROG_ID -s $Path | grep uri | sed 's+\"++g' | sed 's+/++g' | sed 's+,++g' | sort -V | tail -1", returnStdout: true).trim()

return resp
 
}
