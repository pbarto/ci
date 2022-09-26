# genesys-cloud-reception
Genesys Cloud Reception is an example of how you can use a combination of the APIs and Notification subscriptions to enable a UI inside the Genesys Cloud native interface that dynamiclly builds out HTML elements to show users Presence, phone status and one click transfers to the user all in onc view. This is inline with the older physical phones "DSS" buttons that were used for years on reception desks. This is designed as an example only and has no official support. I have removed agent names and replaced them with "Fake Name" for the screen shot. The "Phone" Icon will light up RED when that user is on a phone call either an ACD or NON-ACD call.

![](/docs/images/screenShot1.png?raw=true)

This example uses "Implicit Grant" OAuth2 to your Genesys Cloud ORG environment. The first thing you will need to do is to get a ClientID from your Genesys Cloud ORG with the ability to connect to the API endpoints. This will also need to have a redirect to the Hosting location of the server url for example: "http://localhost:3333/reception.html". You will also need add the required "scopes" for the endpoints that you want to use. In this example we are using "Streaming-events", "analytics", "presence", "users" & "conversations".

![](/docs/images/screenShot2.png?raw=true)

Once you have Created your OAuth you will need to create a "Group" to enable the users that need to have access to this new menu option visable. I would also set the visability to be for members only. 

![](/docs/images/screenShot3.png?raw=true)

Now create the "Client Application" Integration and under the configuration set the URL to the full URL including the paramiters that are required from above: "clientId", "redirectURL", "region"

```
http://localhost:3333/reception.html?gc_region=mypurecloud.com.au&gc_clientId=ENTER_YOUR_ID&gc_redirectUrl=http://localhost:3333/reception.html
```

![](/docs/images/screenShot4.png?raw=true)

Before you load the file you will need to create a file called "config.js" and put it in the root directory. This file needs to be formatted in an array like below. Simply replace the email address with the users, you can add more objects in the array.

```
var contacts = [{
    "email": "test1@test.com"
}, {
    "email": "test2@test.com"
}, {
    "email": "test3@test.com"
}]
```

These email addresses need to be of the users you want to show in the reception view. The email address need to be in the users "profile". The HTML elements are set to dynamicly take up the space that they can so it you make the view full screen there will be more columns of icons the same goes for smaller there would only be one column. The rows will then build out as far as the config.js array of objects is. if this goes beyond the height of the screen a scroll bar will appear to enable more HTML elements to appear.

**NOTE:** If you create a KVP in the "localStorage" of your browser called "gc_debug" with the value of "true" this will enable extra debug logging to appear in the browser console log. This can be handy for testing. 