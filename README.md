# StockHiker <img src="https://github.com/legendkong/StockHiker/blob/main/stockhiker.jpg" width="50" height="50">
A telegram bot for stock alerts.

## Application code
<li> Python
  
## Others
Built using : [Replit](https://www.replit.com/~)
  
## Notes
The main focus of this project is to display the execution of workflow each time somebody commits a change via the use of *GitHub Actions' CI/CD*. <br>
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
When you’ve set your repository to start running this action, any time you open a pull request, it will start linting the code case and return via the Status API. It will let you know if any of your code changes passed successfully, or if any errors were detected, where they are, and what they are. This then allows the developer to go back to their branch, fix any issues, and create a new push to the open pull request. At that point, the Super Linter will run again and validate the updated code and repeat the process. You can configure your branch protection rules to make sure all code must pass before being able to merge as an additional measure. <br>
    
*Wait...what the heck is a lint even?*<br>
------------------    
Lint, or a linter, is a static code analysis tool used to flag programming errors, bugs, stylistic errors and suspicious constructs.[4] The term originates from a Unix utility that examined C language source code. Check out the full meaning behind *lint* [here](https://www.en.wikipedia.org/wiki/Lint_(software)).
    
    
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
  
 


