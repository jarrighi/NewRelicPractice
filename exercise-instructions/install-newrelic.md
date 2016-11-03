## Adding New Relic to the Ruby Kata App

There are 3 steps to installing an APM agent.

1. Adding the New Relic agent library to your application, in this case installing the newrelic_rpm gem
2. Configuring the agent to report with your license key and an application name
3. Redeploying your application so that the newly integrated agent starts up alongside it. 

General instructions for installing the New Relic Ruby Agent can be found [here](https://docs.newrelic.com/docs/agents/ruby-agent/installation-configuration/ruby-agent-installation)

Here are instructions specific to our setup: 

1. To install the newrelic_rpm gem: 

	Use a text editor to add the following line to your newrelic-ruby-kata/Gemfile and save.

	```
	gem 'newrelic_rpm'
	```
	
	Run bundler again. Bundler will notice, download, and install the newly added gem.

	```
	$ bundle install
	```


2. To configure the agent:
	
	Add a newrelic.yml configuration file with your license key to the config directory of your Ruby app.

	* You can use the `initial_newrelic.yml` file here as a template. Copy the contents of the 'initial_newrelic.yml file to the `newrelic-ruby-kata/config` directory. 
	* You can also download a fresh one from your account setting page in rpm.newrelic.com. 

	Make sure the following are true: 

	* the file is named `newrelic-ruby-kata/config/newrelic.yml`
	* the license key for your personal account is in the file (you can find this on your account settings page)
	* monitor mode is set to true for the environment you're running in (probably development)
	
3. To redeploy the application server
	
	```
	rails server -b 0.0.0.0
	```
	
## Checking for success

If all goes well you should see a new application show up in your New Relic APM Application list. If your account number was 0000, the url for this page would be rpm.newrelic.com/accounts/0000/applications. 

You can also find a link to the application overview page in the `newrelic-ruby-kata/logs/newrelic_agent.log`. The log message will look like this:

```
[11/03/16 17:39:31 +0000 vagrant-ubuntu-trusty-64 (2400)] INFO : Reporting to: https://rpm.newrelic.com/accounts/[account_id]/applications/[application_id]
```
