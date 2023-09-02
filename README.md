# Scraping your app analytics data from AppStoreConnect

Hello everyone,

In this project I adress the issue of the AppStoreConnect API not allowing you to recover the analytics data of your app, but only the sales and financial data.

In the notebook are detailed the steps to scrap the analytics data using Selenium.

**DISCLAIMER**

While this solution works to automatically fetch the disered data, it is hardly recomendable in a professional production environment:
- It uses a bot to connect to AppStoreConnect, and the bot needs to be told specifically where to click on the webpage. This means that if Apple makes any change to their website's front, the bot won't work anymore and you will need to change this part in the code.
- If you have sms double authentication set up (like I have), you will need to instanciate the bot on a specific Chrome profile that has verified this double authentication process. The "verified" profile status has a three week or so lifetime, so you will need to update the verified Chrome profile once every three week.

To run the notebook:
- Clone repository
- Create virtual env
- pip install -r requirements.txt
- Create and fill a config.json file at the root of your repository (The parameters needed are detailed bellow)
- Run notebook

The keys you need to provide in the config.json file are the following:

- "email_address_login": address used to login to AppStoreConnect

- "passord_login": password used to login to AppStoreConnect

- "profile_path": You can find your Chrome profile's profile path by going the this url: chrome://version/ while logged in to your profile. If your profil path is C:\Users\user\AppData\Local\Google\Chrome\User Data\Profile 1, then "profile_path" = "C:\Users\user\AppData\Local\Google\Chrome\User Data"

- "profile_directory": Last directory of your profile path. In the example above, "profile_directory" = "Profile 1"

- "adam_id": your app's adam id. You can find it in the url of the website when clicking on your app in AppStoreConnect.

- "cookie_header": the non-resetting parameters of the cookie needed to recover the data. Those are: s_fid, s_vi, XID, POD, accs, dssf; AMCV_something, geo, s_cc, dslang, site, dc, itcdq, s_sq. Your can find them by opening Chrome's developper's tools, going under the "indicators" tab of the app analytics page, and going under "network" of the dev tools. You will find an object called "time-series", this is where you need to click. Then go to "Headers" and fetch the corresponding parameters under "Request Headers"/"Cookie". Your adam id can also be found under the "Payload" part of the "time-series" object.

To recover the measure's names and filters you want to apply to your data before fetching it:

- In the indicator tab, apply any filter you want.
- In Chrome's dev tools, go to the network tab and click the time-series object. You might need to reload the page (ctrl + r on windows)
- Under Payload, you will find the request payload (click on "view source") that you need to parse in the "payload" variable of the notebook, under the "Data fetching" part. 
FYI, you will find in the payload the "measures" you want to recover and the "dimensionFilters" if you applied any filter. The "optionKeys" will be the values that you assigned to these filters.

The reason I am calling my measures separately (using a for loop) in the notebook is because I had trouble fetching more than 2 measures at once.

Thank you for your interest in this tiny project!
