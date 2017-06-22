# Setting up Jenkins

[Getting started with Pipelines](https://jenkins.io/doc/pipeline/)

Jenkins is like CRON, but on steroids

It's awesome to automate things, mundane things, boring things

Download a `.war` file from the downloads page. Place it in a directory of your choice and run

    java -jar jenkins.war

Export JAVA_HOME env variable:

    export JAVA_HOME=/usr/lib/jvm/default-java

You should have `java` (version 1.7 or greater) installed and running.

The first time, it'll give you a first administrator password. When you visit http://localhost:8080/ it will ask you for that password. After entering the password, you'll be asked to install some plugins.

Everything is installed in `~/.jenkins` folder. No database. If you delete this folder, you'll start from scratch.

Then, you need to create the admin account.

Go to Manage Jenkins > Configure Global Security to configure authorization and authentication

Go to Manage Jenkins > Manage Users to add/remove users

## Docker

That's a very convenient way of running Jenkins. There is a hub in http://hub.docker.com with Jenkins images and there is documentation too about how to install and how to run Jenkins in a docker container.

# Creating application builds

Clone the repo https://github.com/g0t4/jenkins2-course-spring-boot.git

Go to `spring-boot/spring-boot-samples/spring-boot-samples-atmosphere`. You'll build that project with Maven

Install Maven

`mvn compile` to compile the Java code

`mvn test` to run tests

`mvn test` to run tests

`mvn package` to package your app in a `.war` o `.jar` file

In the project configuration, go to *Source code management*, and enter the URL for the repo

Then, go to *Build* and add a build step, *Maven targets*, especifying `compile` as maven target and `spring-boot-samples/spring-boot-sample-atmosphere/pom.xml` the target POM file

*Project view*: the page where options about the project or job are shown

*Build view*: the page where you can see optoins for a specific build

*Console view*: to see what commands are executed

*Workspace*: source code of our project. `JENKINS_HOME/jobs/<job name>/workspace`

From the Project view, you can navigate the project's workspace

The workspace is common for the project, so files may be modified from build to build

A way to keep interesting files (for example, a `.jar` file with our app) we need to configure a *Post-Build step* to *Archive artifacts*

The archived artifact will be shown in the Project view in this case. It depends on what type of artifact and what plugin do you use

**What's the difference between a Job and a Build?** A Job is defined by a configuration file. A Job can be seen as a step in the build process of our application. A Job can have multiple Builds associated with it. A Build is the result of executing a Job.

# Testing and CI

Add build steps to your project: execute shell script, run maven target,...

Add build triggers or build post-build actions

But that way is the *old* way. We're going to take a look at the modern way, the Pipeline way.

When creating a Pipeline project, there is no *build* step, or *post-build* actions step. Instead, there are advanced options and *pipeline* steps.

Pipelines are described in Groovy scripts.

In Pipelines, there is a command, `step`, that includes all standard steps for Free Style projects.

```
node {
    git branch: '*/master', url: 'https://github.com/g0t4/jenkins2-course-spring-boot.git'
    
    def projectPath = 'spring-boot-samples/spring-boot-sample-atmosphere'
    dir(projectPath) {   // run commands in a custom workind directory
        sh 'mvn clean package' // run shel command
    
        archiveArtifacts 'target/*.jar'  // archive .jar files
    }
}
```

"Master Agent model" sub-chapter is really interesting.

Something interesting about pipelines are *Stage view*. You can add a stage to the Pipeline script with:

```
stage 'Stage name'
...
```

Absolutely fantastic! In the project view, you can see a graph/table/visual-thing about what stages have been successful, what ones have failed, how much time they took to run,... Impresive!

Email notification in a Pipeline

Choose step `emailext`

One can define functions in Pipeline scripts. Awesome! You can define a `notify` method:

```
def notify(status) {
  emailext(
    to: 'rchavarria@whatever.com',
    subject: "Job ${env.JOB_NAME}",
    body: "${status}"
  )
}
```

Notify on errors

As the pipeline script is just a groovy script, we can use `try-catch` blocks. Hmmm, this sound weird to me, but ok.

Visualizing test results: through the traditional step of "Publish JUnit..."

# Finding and managing plugins

# Building continuous delivery pipelines

# Summary


