# Scraping your app analytics data from AppStoreConnect

Hello everyone,

This project adresses the issue of the AppStoreConnect API not allowing you to recover the analytics data of your app, but only the sales and financial data.

In the notebook are detailed the steps to scrap the analytics data using Selenium.

<span style="color:red">DISCLAIMER</span>

While this solution works to automatically fetch the disered data, it is hardly recomendable in a professional production environment:
- It uses a bot to connect to AppStoreConnect, and the bot needs to be told specifically where to click on the webpage. This means that if Apple makes any change to their website's front, the bot won't work anymore and you will need to change this part in the code.
- If you have sms double authentication set up (like I did), you will need to instanciate the bot on a specific Chrome profile that has verified this double authentication process. The "verified" profile status has a three week or so lifetime, so you will need to update the verified Chrome profile once every three week.

To run the notebook:
- Clone repository
- Create virtual env
- pip install -r requirements.txt
- Create and fill a config.json file at the root of your repository (The parameters needed are detailed bellow)
- Run notebook

