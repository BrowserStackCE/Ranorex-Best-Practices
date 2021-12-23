# Ranorex-Best-Practices
				  	         	

## Getting Started with Browserstack
This guide is meant to provide Ranorex specific information to help you have a smoother experience on Browserstack.
## Index
### 1. [General best practices](#General-Best-Practices).
### 2. [Frequent Issues](##Frequent-Issues).
- Issues with KeySequences and PressKeys.
- Clicks not working.
- Clear text field

## General-Best-Practices
1. Start browser window in maximised mode while recording the tests and when executing the same.
2. [Start Selenium Server on your local machine.](https://www.ranorex.com/help/latest/interfaces-connectivity/selenium-webdriver-integration/)

## Frequent-Issues
1. [mouse click not working](##Bug-1)
2. [execute clear text field](##Bug-2)
3. [execute presskey for String and then Enter key](##Bug-3)

## Bug-1
Click is based on coordinates called ActionSpot. If resolution is not the same, coordinates would change. 
The window size and resolution should be the same while recording the session in the local machine and while execution of the session on browserstack.

- [Prerequisites for successful recording](https://www.ranorex.com/help/v9.5/ranorex-studio-fundamentals/ranorex-recorder/recording-a-test/#:~:text=the%20screencast%20now-,Steps%20for%20successful%20recording,-Ranorex%20Studio%20supports).
We can ensure this by passing Maximized as True

- I confirmed my local machines Screen Dimensions from the .rxlogs. (XXXX x YYY). And passed the capability:
``` resolution" : "XXXX x YYY".```

## Bug-2
You may have a hard time executing key combinations,  due to delays and waits not being properly applied.
Certain key combinations are not supported by Ranorex on remote web driver.
Found it to be a Ranorex issue. 

### Option 1 : 
For Key Combinations, I created a User code and used Selenium commands in it. 
Note:
- It is necessary to have the selenium server running to execute the Selenium commands or it may not work on your local machine.
- Ranorex recommends using mouse click instead of tab key for navigation.



### Option 2 : 
Another solution which will work on ranorex locally and on browserstack is to use javascript executors.
- For the use case of clearing out forms (where ctrl+A was not working), user can do something like (domain used here is the one being used in test sessions below, and to be replaced with user’s website):
```sh
WebDocument  wdd = @"/dom[@domain='the-internet.herokuapp.com']";
wdd.ExecuteScript("document.getElementById('target').value=''");
```
 
- They can also select the form and clear it.

## Bug-3
For enter I used PressKeys("{Return}" and that worked successfully. You may also use Key Sequence {Return}  
Sharing the [link](https://drive.google.com/drive/u/5/folders/1p267FXFaCFW-ofvi9u2_UXFKoEaDzB7A) to the project, containing the test under name of Recording1.cs, along with a video of the Local run and on Browserstack 
- Imp. Pointers:
You can pass the capability "browserstack.selenium_version" : "3.14.0", to do so.
- The [capability builder](https://www.browserstack.com/automate/capabilities) page automatically suggests the right version based on the device. 


## Resources
Links :
- [Ranorex Selenium Webdriver Integration](https://www.ranorex.com/help/latest/interfaces-connectivity/selenium-webdriver-integration/)
- [Capability Builder](https://www.browserstack.com/automate/capabilities)


