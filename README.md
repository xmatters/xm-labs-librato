# Librato
[Librato](http://www.solarwinds.com/librato) aggregates cloud metrics into real-time monitoring dashboards for instant visibility. 

This integration extends the alerting capability of Librato to leverage the xMatters communications platform and toolchain capabilities. 

---------

<kbd>
  <a href="https://support.xmatters.com/hc/en-us/community/topics">
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
  </a>
</kbd>

---------


# Pre-Requisites
* [Librato](http://www.solarwinds.com/librato) account
* xMatters account - If you don't have one, [get one](https://www.xmatters.com)!

# Files
* [LibratoCommPlan.zip](LibratoCommPlan.zip) - Workflow containing the inbound integration and form templates

# How it works
An alert fires a webhook to the xMatters integration builder. The integration builder parses the incoming json and builds the event, then fires the event to notifiy the default recipients. Alternatively [subscriptions](http://help.xmatters.com/OnDemand/userguide/receivingalerts/subscriptions/howtousesubscriptions.htm) can be set up to notify the desired parties. 

# Installation


## xMatters set up
1. Login as a Company Supervisor and navigate to the Developer tab. 
2. Import the [LibratoCommPlan.zip](LibratoCommPlan.zip) file and update the access permissions to include the `REST Web Services User` role. 
3. Click on the Integration Builder tab and click on the `Inbound from Librato` link. Scroll to the bottom and copy the trigger url at the bottom. Save for later. 
4. Go back to the Forms tab and click the Edit > Layout next to the `New Librato Alert` form. Populate the recipients section with the desired recipient. 

## Librato set up
1. Login to Librato and navigate to Alerts

<kbd>
  <img src="media/LibratoAlerts.png">
</kbd>
2. Click Create New Alert and enter the appropirate information Alert name, description, and runbook url. Then add the Alert conditions the alert should be triggered for. 
3. On the Notification Services tab click the Create New Service drop down and scroll down to Webhook

<kbd>
  <img src="media/LibratoCreateService.png">
</kbd>

4. Enter a title and in the url field, paste in the Inbound Integration url copied from xMatters above. 

<kbd>
  <img src="media/LibratoWebhook.png">
</kbd>

5. Click Save. Send a test alert to make sure everything is working.

# Testing
Do some actions in your application or infrastructure that will trigger the alert conditions set up in the Alert. This will fire a webhook into the inbound integration builder script and an event will be created, targeting the default recipients. 

# Troubleshooting
The first place to start is in the Alert, on the Notification Services tab, click the `Test Fire Alert` button. Read the Activity Stream for the `Inbound from Librato` integration script and check for any errors. If nothing is making it to the activity stream, verify the url is correct, paying special attention to the `apiKey` at the end. If the webhook is successful and activity is occuring in the Activity Stream, then review for any errors posting the event. 

