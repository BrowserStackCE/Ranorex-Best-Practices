# Ranorex-Best-Practices
				  	         	

## Getting Started with Browserstack
This guide is meant to provide Ranorex specific information to help you have a smoother experience on Browserstack.
## Why this doc?
## General best practices.
## Frequent Issues and their resolutions:
Issues with KeySequences and PressKeys.
Clicks not working.
Clear text field
## RESOURCES:
Links
## Why this doc?
There are some common issues when using Ranorex on Browserstack. This document will aim to resolve these issues.

## General Best Practices : 
Start browser window in maximised mode while recording the tests and when executing the same.
Start Selenium Server on your local machine.  https://www.ranorex.com/help/latest/interfaces-connectivity/selenium-webdriver-integration/

## Frequent Issues and their resolutions
mouse click not working
execute clear text field
execute presskey for String and then Enter key 

## Bug 1 - mouse click not working
Click is based on coordinates called ActionSpot. If resolution is not the same, coordinates would change. 
The window size and resolution should be the same while recording the session in the local machine and while execution of the session on browserstack.

## Prerequisites for successful recording 
https://www.ranorex.com/help/v9.5/ranorex-studio-fundamentals/ranorex-recorder/recording-a-test/#:~:text=the%20screencast%20now-,Steps%20for%20successful%20recording,-Ranorex%20Studio%20supports
We can ensure this by passing Maximized as True

I confirmed my local machines Screen Dimensions from the .rxlogs.
And passed the capability: resolution" : "1440x900", as mentioned below.

## Bug 2 - Execute key combinations (clear text field)
You may have a hard time executing key combinations,  due to delays and waits not being properly applied.
Certain key combinations are not supported by Ranorex on remote web driver.
Found it to be a Ranorex issue. 

### Option 1 : For Key Combinations, I created a User code and used Selenium commands in it. It is necessary to have the selenium server running to execute the Selenium commands or it may not work on your local machine.
Ranorex recommends using mouse click instead of tab key for navigation.



### Option 2 : 
Another solution which will work on ranorex locally and on browserstack is to use javascript executors.
For the use case of clearing out forms (where ctrl+A was not working), user can do something like (domain used here is the one being used in test sessions below, and to be replaced with user’s website):
WebDocument  wdd = @"/dom[@domain='the-internet.herokuapp.com']";
wdd.ExecuteScript("document.getElementById('target').value=''");
 
They can also select the form and clear it.

## Bug 3 - execute presskey for String and then Enter key 
For enter I used Key Sequence {Return} and that worked successfully.
Imp. Pointers:
You can pass the capability "browserstack.selenium_version" : "3.14.0", to do so.
The capability builder page automatically suggests the right version based on the device. https://www.browserstack.com/automate/capabilities


## RESOURCES
Links
https://www.ranorex.com/help/latest/interfaces-connectivity/selenium-webdriver-integration/
https://www.browserstack.com/automate/capabilities


