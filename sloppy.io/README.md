# Deploying Rocket.Chat to sloppy.io

<p><a href="http://sloppy.io"><img src="http://sloppy.io/wp-content/uploads/2014/04/sloppy-icon.png" align="top" height="300" width="300" ></a></p>


[sloppy.io](http://sloppy.io) is a CaaS (Container as a Service) Provider. You can deploy, scale and manage your dockerized applications in seconds. [Try it for free](http://sloppy.io/#signup) 

## Start it

```
sloppy start rocketchat.json  -var=USERNAME:yourusername,URI:mydomain.sloppy.zone
   
Example:
   
sloppy start rocketchat.json  -var=USERNAME:john,URI:coolchat.sloppy.zone
```