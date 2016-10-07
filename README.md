# New Relic Ruby Practice Environment

We'll use this environment in training to practice installing the New Relic agent and setting up custom data.

## Getting Started

These instructions will get you a copy of the practice environment up and running on your local machine. This environment is meant to be run locally for learning purposes, not in production. 

### Prerequisities

[Use these instructions to download and install Virtualbox for your operating system](https://www.virtualbox.org/wiki/Downloads)

[Use these instructions to download and install Vagrant for your operating system](https://www.vagrantup.com/downloads.html)

Once you have those installed, clone this repository and get started with the setup instructions below.

### Create you vagrant box

Move into the cloned repository

```
$ cd newrelic-support-training-apps
```

You should see the following items in this directory

```
$ ls
Vagrantfile
README.md
newrelic-ruby-kata
```
The Vagrantfile will allow us to create a virtual machine with Vagrant where you will do most of the lab work for this course. 

The directories in this folder will be accessible from the virtual machine and contain the app and scripts we will use for our labs.

To spin up the virtual machine, run

```
$ vagrant up
```

Once the box has been created you shoudl see that a `.vagrant` directory has been created and you can now ssh into that machine

```
$ vagrant ssh
```

Once you've signed in to the machine, you're ready to start setting up the Rails app.

### Setting up the Ruby Kata App

#### Setup a postgres user 

```
$ sudo su postgres
$ createuser -s -W vagrant
```

Set your password when prompted
Now that a vagrant user has been created in postgres, you can go back to the vagrant user. 

```
$ exit
```

#### Configure the app to connect to postgres and load data

```
$ cd /vagrant/newrelic-ruby-kata/
```

edit the config/database.yml to reflect that password

```
$ bundle install
$ bundle exec rake db:create
$ pg_restore --verbose --clean --no-acl --no-owner -h localhost -U vagrant -d newrelic-ruby-kata_development public/sample-data.dump
```
enter your password when prompted

#### run the app

```
$ rails server -b 0.0.0.0
```

you should be able to visit the app in your browser now by going to `http://localhost:3030/`. 
Try visiting the loop page as well to verify the database is setup properly. 

If you get an error on the page, there was probably a problem loading the sample data into postgres

## Adding New Relic to the Ruby Kata App


## Setting up the Insights exercises

TODO 




