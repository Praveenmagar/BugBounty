# Walking an Application

- As a penetration tester, your role when reviewing a website or web application is to discover features that could potentially be vulnerable and attempt to exploit them to assess whether or not they are.

## Viewing Page source
- It is human-readable code returned to our browser/client from the web server each time we make a request
- Here, pick out bits of information that are of importance to us
    - Below are the comments left by the website developer, usually to explain something in the code to other programmers or even notes/reminders for themselves
        ```
        <!-- and ending with -->
        ```
    - See different anchor tag links
    - Today websites aren't made from scratch and use what's called a framework
    - Viewing the page source can often give us clues into whether a framework is in use and, if so, which framework and even what version.

## Developer tool : Inspector
- This tool is used to aid web developers in debugging web applications and gives you a peek under the hood of a website to see what is going on
- Most important three features
    - Inspector, 
    - Debugger and 
    - Network
- View page source doesn't always represent what's shown on a webpage due to CSS, JS and user interactions
- Inspector 
    -  Inspector assists us with this by providing us with a live representation of what is currently on the website
- Example: 
    - Right click and inspect and check for
        ```
        display:block;
        ```
    - and change this to
        ```
        display:none;
        ```

## Developer tool: Debugger
- It gives us the option of digging deep into the JavaScript code
- In Firefox and Safari, this feature is called Debugger, but in Google Chrome, it's called Sources

## Developer tool: Network
- Used to keep track of every external request a webpage makes
- If you click on the Network tab and then refresh the page, you'll see all the files the page is requesting. 