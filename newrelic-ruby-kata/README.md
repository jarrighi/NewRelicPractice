newrelic-ruby-kata
==================

Using New Relic, see how many things you can find and fix to make this app perform fast!

This is a modified version of the New Relic Ruby Kata application. The main version of this app can be found on [Github](https://github.com/newrelic/newrelic-ruby-kata)

Step 1
-------
Load the sample DB locally:

    bundle exec rake db:create
    pg_restore --verbose --clean --no-acl --no-owner -h localhost -U $USER -d newrelic-ruby-kata_development public/sample-data.dump
    bundle exec rails s

Step 2
-------
You can watch a [video on getting started](https://learn.newrelic.com/courses/intro_apm/performance_apm) with the New Relic agent to help get you started. The New Relic agent will help you find and solve the performance issues in this application as well as help you see the complete impact of your changes.

Step 3
-------
Fix the code / Solve as many of the Katas as you can. There are seven distinct Katas in this application that can be torn apart and fixed by using your awesome dev abilities and the deep metrics that New Relic provides.

