# StockHiker <img src="https://github.com/legendkong/StockHiker/blob/main/stockhiker.jpg" width="50" height="50">
A telegram bot for stock alerts.

## Application code
<li> Python
  
## Others
Built using : [Replit](https://www.replit.com/~)
  
## Notes
The main focus of this project is to adopt the DevOps culture to display the execution of workflow each time somebody commits a change via the use of *GitHub Actions*. <br>
  <img src="https://github.com/legendkong/StockHiker/blob/main/images/GitHub_Actions.png" width="200" height="120"><br>
I created two seperate workflows:
  <li> Super-linter
  <li> Telegram notifier  
  
  
## Main Application 
  
Using python, I created a telegram bot that allows the user to receive real time stock data(latest 5 minutes) of their desired stock by typing <ins>*price {ticker symbol}*</ins>.<br>
  <p align="center">
  <img src="https://github.com/legendkong/StockHiker/blob/main/price2.gif" width="350" height="520">
  </p>
  <br><br>
The user is also able to retrieve the stock data of their top 3 stock picks(implemented within the code itself) just by typing a simple <ins>/wsb</ins> command.
  <br>
  <p align="center">
  <img src="https://github.com/legendkong/StockHiker/blob/main/wsb3.gif" width="350" height="520">
  </p>
  <p align="center">
  <em>In this case, stock ticker symbol "TSLA", "NIO" and "PLTR" are the user's favourite stock picks.</em>
  </p>
  <br><br>
  
 # Workflow 1 *(Super-linter)*
    
*What is it?*<br>
------------------
The Super Linter is a source code repository that is packaged into a Docker container and called by GitHub Actions. This allows for any repository on GitHub.com to call the Super Linter and start utilizing its benefits. <br><br>
    
*How it works*<br>
------------------
When you’ve set your repository to start running this action, any time you open a pull request, it will start linting the code case and return via the Status API. It will let you know if any of your code changes passed successfully, or if any errors were detected, where they are, and what they are. This then allows the developer to go back to their branch, fix any issues, and create a new push to the open pull request. At that point, the Super Linter will run again and validate the updated code and repeat the process. You can configure your branch protection rules to make sure all code must pass before being able to merge as an additional measure. <br><br>
    
*Wait...what the heck is a lint even?*<br>
------------------    
Lint, or a linter, is a static code analysis tool used to flag programming errors, bugs, stylistic errors and suspicious constructs. The term originates from a Unix utility that examined C language source code. Check out the full meaning behind *lint* [here](https://www.en.wikipedia.org/wiki/Lint_(software)).
    
    
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
<img src="https://github.com/legendkong/StockHiker/blob/main/images/super-linter1.PNG"> <br>
    <p align="center">
  *As you can see from the above image, my main.py (main application code) and other commits failed all super-linter tests.*:sweat_smile: *Let's find out why.*
    </p>
<br><br>
    

-----------------------------------------------------------------------------------------------------------------------------------------------------------------
  <img src="https://github.com/legendkong/StockHiker/blob/main/images/super-linter2.PNG"> <br>
    <p align="center">       
    *Passed all tests except the "Run Super-Linter" step*	:thinking:
     </p>
<br><br>
    
 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------   
 <img src="https://github.com/legendkong/StockHiker/blob/main/images/super-linter3.PNG"> <br>
    <p align="center">       
    *Realised that there's ~~some~~ many syntax errors in the main code, hence didn't pass the super-linter test*:hot_face:
     </p>
<br><br>
 
    
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
  <img src="https://github.com/legendkong/StockHiker/blob/main/images/super-linter4.PNG"> <br>
    <p align="center">       
    *Notice that there is a red cross on the top right corner of the main page of repository. This shows that the super-linter workflow is active, and the red cross represents the pass/fail state of the latest test.*
     </p>
<br><br>
    
# Workflow 2 *(Telegram notification)*
    
*What is it?*<br>
------------------
The Telegram Custom Message Action will be added to my repository such that a notification would be sent to my telegram bot when some actions are triggered. (Push, Pull request)   <br><br>
    
*How it works*<br>
------------------   
 1. Create a Telegram Bot using [BotFather](https://t.me/botfather) 
 2. Get your Token Key after creating the bot. I cancelled out the token key for the sake of privacy.
     <p align="center">
  <img src="https://github.com/legendkong/StockHiker/blob/main/images/token-key-telegram-new.jpg"></p><br>
    
 3. Use secrets variable to store the Telegram bot token and our chat identifier key (in order to know who to notify when there is a change in the GitHub repo status). Visit the following URL on your web browser:
    https://api.telegram.org/bot*TokenID*/getUpdates 
    where *TokenID* is your telegram token key.
 
 4. Get the unique chat id from the JSON output.
    <p align="center">
      <img src="https://github.com/legendkong/StockHiker/blob/main/images/jsonkey.PNG"></p> <br>

 5. Add variables *TELEGRAM_TO* and *TELEGRAM_TOKEN* into the Secrets of your repository, where *TELEGRAM_TO*'s value is your unique chat id and *TELEGRAM_TOKEN* is your token key.
    
 6. Set up a new workflow under GitHub Actions within your repository. Update the name from "main.yml" to "tg-notify.yml". Replace the code with the one as shown below.
    <p align="center"> 
```
name: tg-notify
on: [push, pull_request]
  
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Update status
      uses: appleboy/telegram-action@master
      with:
        to: ${{ secrets.TELEGRAM_TO }}
        token: ${{ secrets.TELEGRAM_TOKEN }}
        message: |  #https://help.github.com/en/actions/reference/contexts-and-expression-syntax-for-github-actions#github-context
          ${{ github.event_name }} commit in ${{ github.repository }} by "${{ github.actor }}". [${{github.sha}}@${{ github.ref }}]
```
    
    
What the following workflow does is that it sends the user a notification via Telegram when the repo have a new push commit or pull request. The message would contain the commit status (either a push or pull request) with the repo name, followed by the username of the person who triggered the workflow. 
    <br><br>
    
7. Click on "Start commit" and select "Commit New File". This will create the work flow and start GitHub Action!:relieved:
    
     <p align="center">
       <img src="https://github.com/legendkong/StockHiker/blob/main/images/telebotfinal.gif"></p> <br>
    <p align="center">       
   My telegram bot updates me whenever somebody commits something into the repository!:partying_face:
     </p>
<br><br>
    
 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
    
    
# Credits
[Uli](https://www.github.com/u1i) for introducing me to the world of DevOps. <br>
[Cyan Infinite](https://www.cyaninfinite.com/getting-updates-from-github-via-telegram-bot/) for documentation of implementation of Telegram Notification Bot. <br>
[DevOps Journey](https://www.youtube.com/watch?v=mFFXuXjVgkU&t=329s) for super-linter tutorial.

