//@Library('shared-library@master') _
pipeline {
   agent any
   environment {
      int BN =  buildnumber1(JFROG_ID)
         JFROG_ID = credentials('jfrogid')
    url = "https://jfrgfreetst.jfrog.io/artifactory/api/storage/example-repo-local"
	   url_new = "https://jfrgfreetst.jfrog.io/artifactory/api/storage/example-repo-local/?sort"
    //folder_path = curlmethod(url,JFROG_ID,BN)
    //Path = "${url}/${folder_path}/?sort"
   //image_name = curlmethodnew(Path, JFROG_ID)

      }


   stages {
      stage('Passing Values to Child Job') {
         steps {


			script{
				def int intval = BN
				echo "$intval"
				i = 1
				def NSN = []
				//def Path = "${url}/NSN[y]/?sort"
				//def RL = curlmethodnew(Path, JFROG_ID)
				while(i < (intval + 1)) {

				def f = curlmethod(url_new,JFROG_ID,i);
				NSN.add(f);
				i++;

				}
				z = 0
				//def Path = "${url}/NSN[y]/?sort"
				def RL = []
				while(z < intval) {
				def Paths = "${url}/${NSN[z]}/?sort";
				b = curlmethodnew(Paths, JFROG_ID);
				RL.add(b);
				z++;
				}



				

print NSN
print RL
			for (p in 1..intval) {
				// add your child job below which has to be triggered and pass the parameters
					//xz = "${i}"
					//def SN = ["Renuka","Prasad","Deepu"]
					def y = p - 1


				//	response = null
					//def Paths = "${url}/NSN[y]/?sort"
					//def RLS = curlmethodnew(Paths, JFROG_ID)
					//print(Path, RLS)



					build job: "env_test_myjenk", wait: false, parameters: [
					string(name: 'SERVICE_NAME', value : NSN[y]) ,
					string(name: 'RELEASE_LABEL', value : RL[y] )
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

String resp = sh(script: "curl -u $JFROG_ID -s $Path | grep uri |awk '{print \$3}'| sed 's+\"++g' | sed 's+/++g' | sed 's+,++g'| sort -V |tail -2 |head -1", returnStdout: true).trim()

return resp

}
