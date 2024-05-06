// def pauseExecution(duration) {
//     def milliseconds = duration * 1000
//     Thread.sleep(milliseconds)
// }

def pauseExecution(duration) {
    def startTime = System.currentTimeMillis()
    def endTime = startTime + duration * 1000
    while (System.currentTimeMillis() < endTime) {}
}

pipeline {
    agent any

    parameters {
        string(
            name: "TEST_1",
            defaultValue: "Hello World"
        )
    }

    stages {
        stage("Do") {
            steps {
                script {
                    println "123"
                    println params.TEST_2
                    sh "ls ${WORKSPACE}"
                    sh "echo 123"

                    syncPoints = [:]
                    tasks = [:]
                    tasks["Run"] = {
                        syncPoints["Run"] = 1
                        sleep time: 6, unit: "MINUTES"
                        syncPoints["Run"] = 0
                    }

                    tasks["Check"] = {
                        def timeToGetInfo = 0
                        while(syncPoints["Run"]) {
                            if (timeToGetInfo % 2 == 0) {
                                println "Checking ..."
                            }
                            // sh "#!/bin/sh -e\n" + "sleep 60 > /dev/null 2>&1"
                            pauseExecution(60)
                            timeToGetInfo += 1
                        }
                    }

                    parallel(tasks)
                }
            }
        }
        stage("Done") {
            steps {
                script {
                    sh "echo 456"
                }
            }
        }
    }
}