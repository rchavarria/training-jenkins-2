# Setting up Jenkins

[Getting started with Pipelines](https://jenkins.io/doc/pipeline/)

Jenkins is like CRON, but on steroids

It's awesome to automate things, mundane things, boring things

Download a `.war` file from the downloads page. Place it in a directory of your choice and run

    java -jar jenkins.war

You should have `java` (version 1.7 or greater) installed and running.

The first time, it'll give you a first administrator password. When you visit http://localhost:8080/ it will ask you for that password. After entering the password, you'll be asked to install some plugins.

Everything is installed in `~/.jenkins` folder. No database. If you delete this folder, you'll start from scratch.

Then, you need to create the admin account.

Go to Manage Jenkins > Configure Global Security to configure authorization and authentication

Go to Manage Jenkins > Manage Users to add/remove users

## Docker

That's a very convenient way of running Jenkins. There is a hub in http://hub.docker.com with Jenkins images and there is documentation too about how to install and how to run Jenkins in a docker container.

# Creating application builds

# Testing and CI

# Finding and managing plugins

# Building continuous delivery pipelines

# Summary


