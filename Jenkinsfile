// Documentation: https://github.com/coreos/coreos-ci/blob/master/README-upstream-ci.md

//def imageName =  buildImage()
pod(image: "coreos-ci-coreos-7b93e0e0-bd2f-4663-bc96-d57b480145ea:latest", kvm: true, memory: "10Gi") {

  shwrap("rpm -qa | sort > rpmdb.txt")
  archiveArtifacts artifacts: 'rpmdb.txt'
  fcosBuild(skipKola: 1, cosaDir: "/srv/", noForce: 1)
//  fcosKola(basicScenarios: true, cosaDir: "/srv", addExtTests: ["ci/run-kola-self-tests"])

 stage("Build Metal") {
        cosaParallelCmds(cosaDir: "/srv", commands: ["metal", "metal4k"])
    }
  stage("Build Live Images") {
      utils.cosaCmd(cosaDir: "/srv", args: "buildextend-live --fast")
  }
   stage("Test Live Images") {
       fcosKolaTestIso(cosaDir: "/srv", extraArgs4k: "--no-pxe")
   }
   stage("Build Cloud Images") {
        cosaParallelCmds(cosaDir: "/srv", commands: ["Aliyun", "AWS", "Azure", "DigitalOcean", "Exoscale", "GCP", "IBMCloud", "OpenStack", "VMware", "Vultr"])
   // quick schema validation
        utils.cosaCmd(cosaDir: "/srv", args: "meta --get name")
    }

}

def cosa_cmd(args) {
    shwrap("cd /srv && sudo -u builder cosa ${args}")
} 
