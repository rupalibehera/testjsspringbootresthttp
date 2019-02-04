@Library('github.com/fabric8io/osio-pipeline@master') _

osio {

  config runtime: 'java', version: '1.8'

  ci {
    echo "CI....."
     integrationTestCmd = "mvn verify integration-test -Dnamespace.use.current=false -Dnamespace.use.existing=${testNamespace()} -Dit.test=*IT -DfailIfNoTests=false -DenableImageStreamDetection=true -Popenshift,openshift-it"
     //runTest commands: integrationTestCmd
    spawn 
          image: 'java',
          commands: "java -version",
          envVar: ["a":"b", "MAVEN_OPTS": '-Dorg.slf4j.simpleLogger.log.org.apache.maven.cli.transfer.Slf4jMavenTransferListener=warn']
  }

  cd {

    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])

    build resources: resources
    deploy resources: resources, env: 'stage'
    deploy resources: resources, env: 'run', approval: 'manual'

  }
}
