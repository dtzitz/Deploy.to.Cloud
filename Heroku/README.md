# Deploying Rocket.Chat to Salesforce's Heroku

Heroku is a CloudFoundry based provider.  

Two ways to deploy Rocket.Chat to Heroku:

* easy one click
* customized command line


## One Click automatic deploy


Try clicking the button below, and either login or create a new account, then follow all prompts.

[One-Click Deploy](https://heroku.com/deploy?template=https://github.com/RocketChat/Rocket.Chat/tree/master)

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/RocketChat/Rocket.Chat/tree/master)

If everything goes well, you will have your own instance of Rocket.Chat running.  

If not, please raise an issue.

## Customized command line for developers

This is the option that gives you full control.  It is the preferred option for developers.  

First make sure you have the following installed:

* git
* Heroku CLI

Next, checkout the latest version of Rocket.Chat:

~~~
git clone https://github.com/RocketChat/Rocket.Chat
~~~

Change into the `Rocket.Chat` directory, and create your Heroku app:

~~~
heroku apps:create  --addons mongolab:sandbox,logentries:le_tryit -b https://github.com/RocketChat/heroku-buildpack-meteor <your app name>
~~~

Choose \<your app name> carefully, as your Rocket.Chat will then be accessible at:

~~~
https://<your app name>.herokuapps.com/
~~~

Next, you *MUST* set the ROOT_URL environment variable:

~~~
heroku config:add ROOT_URL=https://<your app name>.herokuapp.com/
~~~

If your app failed to start, check and make sure you have ROOT_URL set.

Heroku app deployment is triggered by git commits - to Heroku's repos, and not github.

You are almost ready to deploy and stage your own instance.  But you must first wire up the git repos to heroku.

~~~
git remote add heroku https://git.heroku.com/<your app name>.git
~~~

Finally, deploy and stage your app by:

~~~
git push heroku master
~~~

Rocket.Chat should now be running.  If you encounter problems, please raise an issue.


### Caveats
* To add any service to an app, even if it is free, you will need to register a valid credit card with Heroku.   Rocket.Chat needs both mongolab and logenteries services.
* Heroku (actually CloudFoundry) uses custom buildpacks to stage applications.  The buildpack used by Rocket.Chat can take a very long time to build - since it needs to download Meteor and build the server image every time.
* You *must*  set the ROOT_URL environment variable, as shown above, otherwise the server side will crash.
* Note mongolab's free sandbox plan does not support oplog tailing - check other plans if you need oplog.
* If you are scaling to multi-dynos on Heroku, and you have clients/customers still using older browsers that do not support WebSocket, you need to be mindful of sticky session support (BETA) on Heroku - see [sticky sessions on Heroku](https://devcenter.heroku.com/articles/session-affinity).
