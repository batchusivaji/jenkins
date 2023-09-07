# Jenkins Declarative Pipeline

## First Declarative Pipeline

## pipeline

```yml
pipeline {
    agent any
    stages {
        stage('Welcome Step') {
            steps { 
                echo 'Welcome to Class'
            }
        }
    }
}
```
## Agent

### agent Any

```yml
pipeline {
     agent any
}
```

### agent none

```yml
pipeline {
     agent none
}
```

### agent label

```yml
pipeline {
       agent {
           label 'linux-machine'
       }
}
```

## stages

```yml
pipeline {
       agent {
           label 'linux-machine'
       }
     stages {
     }
}
```

## stage

```yml
pipeline {
       agent {
           label 'linux-machine'
       }
     stages {
         stage('build step') {
         }
     }
}
```

## steps

```yml
pipeline {
     agent any
     stages {
         stage('build step') {
              steps {
                 echo "Build stage is running"
              }
         }
     }
}
```

## Environment Variables

### Referring Env Variables from Jenkins configuration

```yml
pipeline {
    agent any
    stages {
        stage('Initialization') {
            steps {
                echo "${JAVA_INSTALLATION_PATH}"
            }
        }
   }
}
```

### Creating & Referring Environment variable in Jenkinsfile

```yml
pipeline {
    agent any
    environment {
        DEPLOY_TO = 'production'
    }
    stages {
        stage('Initialization') {
            steps {
                echo "${DEPLOY_TO}"
            }
        }
    }
}
```

### Initialize Env variables using sh commands

```yml
pipeline {
    agent any
    stages {
        stage('Initialization') {
            environment {
                   JOB_TIME = sh (returnStdout: true, script: "date '+%A %W %Y %X'").trim()
            }
            steps {
                sh 'echo $JOB_TIME'
            }
        }
    }
}
```

## credentials

### Loading credentials in declarative pipeline

```yml
pipeline {
    agent any
    environment {
        MY_CRED = credentials('MY_SECRET')
    }
    stages {
        stage('Load Credentials') {
            steps {
                echo "Username is $MY_CRED_USR"
                echo "Password is $MY_CRED_PSW"
            }
        }
    }
}
```

## when

### Simple when block

```yml
pipeline {
     agent any
     stages {
         stage('build') {
              when {
                  branch 'dev'
              }
              steps {
                 echo "Working on dev branch"
              }
         }
     }
}
```

### when block using Groovy expression

```yml
pipeline {
     agent any
     stages {
         stage('build') {
              when {
                  expression {
                     return env.BRANCH_NAME == 'dev';
                  }
              }
              steps {
                 echo "Working on dev branch"
              }
         }
     }
}
```

### when block with environment variables

```yml
pipeline {
    agent any
    environment {
        DEPLOY_TO = 'production'
    }
    stages {
        stage('Welcome Step') {
            	when {
    environment name: 'DEPLOY_TO', value: 'production'
}
            steps {
                echo 'Welcome to Class'
            }
        }
    }
}
```

### when block with multiple conditions & all conditions should be satisfied

```yml
pipeline {
    agent any
    environment {
        DEPLOY_TO = 'production'
    }
    stages {
        stage('Welcome Step') {
            when {
                allOf {
                    branch 'master';
                    environment name: 'DEPLOY_TO', value: 'production'
                }
            }
            steps {
                echo 'Welcome to Class'
            }
        }
    }
}
```

### when block with multiple conditions & any of the given conditions should be satisfied

```yml
pipeline {
    agent any
    environment {
        DEPLOY_TO = 'production'
    }
    stages {
        stage('Welcome Step') {
            when {
                anyOf {
                    branch 'master';
                    branch 'staging'
                }
            }
            steps {
                echo 'Welcome to Class'
            }
        }
    }
}
```

## tools

### Loading maven using tools

```yml
pipeline {
    agent any
    tools {
        maven 'MAVEN_PATH'
    }
    stages {
         stage('Load Tools') {
              steps {
                 sh "mvn -version"
              }
         }
     }
}

```

## parallel

```yml
pipeline {
    agent any
    stages {
        stage('Parallel Stage') {
            parallel {
                stage('windows script') {
                    agent {
                        label "windows"
                    }
                    steps {
                        	echo "Running in windows agent"
		                    bat 'echo %PATH%'
                    }
                }
                stage('linux script') {
                    agent {
                        label "linux"
                    }
                    steps {
                       sh "Running in Linux agent"
                    }
                }
             }
        }
    }
}

```

## post

### post with multiple conditional blocks

```yml
pipeline {
     agent any
     stages {
         stage('build step') {
              steps {
                 echo "Build stage is running"
              }
         }
     }
     post {
         always {
             echo "You can always see me"
         }
         success {
              echo "I am running because the job ran successfully"
         }
         unstable {
              echo "Gear up ! The build is unstable. Try fix it"
         }
         failure {
             echo "OMG ! The build failed"
         }
     }
}
```

## Marking build as UNSTABLE

### Mark build as UNSTABLE based on Code Coverage

```yml
pipeline {
    agent any
    tools {
        maven 'MAVEN_PATH'
        jdk 'jdk8'
    }
    stages {
        stage("Tools initialization") {
            steps {
                sh "mvn --version"
                sh "java -version"
            }
        }
        stage("Checkout Code") {
            steps {
                git branch: 'master',
                url: "https://github.com/batchusivaji000/jenkins.git"
            }
        }
        stage("Building Application") {
            steps {
               sh "mvn clean package"
            }
        }
        stage("Code coverage") {
           steps {
               jacoco(
                    execPattern: '**/target/**.exec',
                    classPattern: '**/target/classes',
                    sourcePattern: '**/src',
                    inclusionPattern: 'com/iamvickyav/**',
                    changeBuildStatus: true,
                    minimumInstructionCoverage: '30',
                    maximumInstructionCoverage: '80')
               }
           }
        }
}
```

## triggers

### triggers sample

```yml
pipeline {
    agent any
    triggers {
        cron('H/15 * * * *')
    }
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
```
