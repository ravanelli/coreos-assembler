// Documentation: https://github.com/coreos/coreos-ci/blob/master/README-upstream-ci.md

//def imageName =  buildImage()
imageName = "coreos-ci-coreos-assembler-b535a6c7-bd9f-47bd-a98d-ec1fd0685cca"
pod(image: imageName + ":latest", kvm: true, memory: "10Gi") {
    checkout scm
    fcosBuild(skipKola: 1, cosaDir: "/srv", noForce: true, gitBranch: "rhcos-4.7")
}
