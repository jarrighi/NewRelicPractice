# New Relic Ruby Practice Environment

We'll use this environment in training to practice installing the New Relic agent and setting up custom data.

## Getting Started

These instructions will walk you through setting up the practice environment and apps on your local machine. This environment is meant to be run locally for learning purposes, not in production. 

### Prerequisities

* **A New Relic account** 
	
	 Make sure it's one you have access to and can send data to. A personal account is best since you may want to experiment with settings. 

* **Virtualbox**

	[Follow this link to download and install Virtualbox for your operating system](https://www.virtualbox.org/wiki/Downloads)

* **Vagrant** 

	[Follow this link to download and install Vagrant for your operating system](https://www.vagrantup.com/downloads.html)

Once you have those three items, clone this repository and get started with the setup instructions below.

```
$ git clone https://github.com/jarrighi/newrelic-support-training-apps.git
```

### Create your vagrant box

Move into the cloned repository

```
$ cd newrelic-support-training-apps
```

You should see the following items in this directory...

```
$ ls
Vagrantfile
README.md
newrelic-ruby-kata
```
The Vagrantfile will allow us to create a virtual machine with Vagrant where you will do most of the lab work for this course. 

The other directories in this folder contain the app and scripts we will use for our labs and they will be accessible from the virtual machine at `/vagrant/`. This means you can use a GUI or terminal based text editor from your host operating system, or a terminal based text editor from within the virtual machine to update the application files. 

To spin up the virtual machine, run

```
$ vagrant up
```

Once the machine has been created you should see that a `.vagrant` directory has been created. 

```
$  ls -A
.git
.gitignore
.vagrant
README.md
Vagrantfile
newrelic-ruby-kata
```

You can now ssh into the virtual machine as the `vagrant` user with the following vagrant command. 

```
$ vagrant ssh
```

Once you've signed in to the machine, you're ready to start setting up the Rails app.

### Setting up the Ruby Kata App

The newrelic-ruby-kata app here is a modified from the one at [github.com/newrelic/newrelic-ruby-kata](https://github.com/newrelic/newrelic-ruby-kata). There are a few more steps we need to follow to get the database setup for this app. 

#### 1. Setup a vagrant user in postgres

We'll need to switch to the postgres user to have the necessary permissions to setup the `vagrant` postgres user.

```
$ sudo su postgres
$ createuser -s -W vagrant
```

The `-W` will allow you to set up a password for this user right away. Set your password when prompted and be sure to write it down. We'll need this password a few steps down. Now that a vagrant user has been created in postgres, you can go back to the vagrant user. 

```
$ exit
```

#### 2. Configure the app to connect to postgres and load data

For the next few steps we'll need to work in the `newrelic-ruby-kata` directory

```
$ cd /vagrant/newrelic-ruby-kata/
```

Below is a summary summary of the files and directories that we will use in this course. 

```
newrelic-ruby-kata
├── Gemfile <- libraries required for this app
├── README.md
├── app <- main application logic
│   ├── assets
│   ├── controllers
│   ├── helpers
│   ├── mailers
│   ├── models
│   └── views
├── config <- New Relic config file will go here
│   ├── application.rb
│   ├── boot.rb
│   ├── database.yml <- add your database user password here
│   ├── environment.rb
│   ├── environments
│   ├── initializers
│   ├── locales
│   ├── puma.rb
│   ├── routes.rb
│   └── secrets.yml
├── config.ru
├── db
└── log <- the NR agent writes its log to this directory
    └── development.log
```

Edit `config/database.yml` to reflect the password you set for your `vagrant` user in postgres. Now the app should be able to connect to the database. Run the following commands to install the ruby libraries for this app.


```
$ bundle install
```

Create the necessary database tables.

```
$ bundle exec rake db:create
```

Load the sample data.

```
$ pg_restore --verbose --clean --no-acl --no-owner -h localhost -U vagrant -d newrelic-ruby-kata_development public/sample-data.dump
```

You'll need to enter your password when prompted

Note: If you have errors related to passwords here, see the section on resetting postgres passwords below.


#### 3. Launch the app to check your setup

```
$ rails server -b 0.0.0.0
```

You should now be able to visit the app in your host machine's browser by going to `http://localhost:3030/`. 

Try visiting the [loop page](`http://localhost:3030/loop`) as well to verify the database is setup properly. 

If you get an error on the page, there was probably a problem loading the sample data into postgres.


## Resetting your postgres user's password

If you have errors related to passwords when setting up the database, you may want to reset your vagrant user's password in postgres. You can do this using the psql tool:

```
$ psql -d postgres
psql (9.3.14)
Type "help" for help.

```

Once you're in psql, you can run the following query.

```
postgres=# ALTER USER "vagrant" WITH PASSWORD 'password';
ALTER USER
```

You can quit psql like this:

```
postgres=# \q
```



