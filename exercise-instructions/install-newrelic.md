## Adding New Relic to the Ruby Kata App

General instructions for installing the New Relic agent can be found [here](https://docs.newrelic.com/docs/agents/ruby-agent/installation-configuration/ruby-agent-installation)

In short: 

1. Install the newrelic_rpm gem.

	Add the following line to your Gemfile 

	```
	gem 'newrelic_rpm'
	```
	
	Run bundler again before you restart your app.

	```
	$ bundle install
	```


2. Add a newrelic.yml configuration file with your license key to the config directory of your Ruby app.

	You can use the `initial_newrelic.yml` file here as a template. Copy this file to the `config` directory in the newrelic-ruby-kata app or download a fresh one from your account setting page in rpm.newrelic.com. 

	Make sure the following are true: 

	* the file is named `newrelic.yml`
	* the license key for your personal account is in the file
	* monitor mode is set to true for the environment you're running in (probably development)