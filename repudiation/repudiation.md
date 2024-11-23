# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
- There is no way to track actions that users have made- mechanisms in a system that hold people accountable for their actions.
- insufficient logging of the reqeusts and responses - have no way of analyzing how services are being accessed
- logs vulnerable to tampering. someone could feed malicious inputs causing a privilege of escalation

2. Briefly explain why the vulnerability is addressed in __secure.ts__.
- insecure.ts logs actions to the console, does not persist on the actions so that when the server goes down or the session ends there is no way of tracking back or invesitagting the problem.
- malicious user could make changes to the system, but the system would not be able to track down the user

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
- Logging based pattern -- request goes to ReqLogger which is is a middleware function, then secure services and log files, then response logger is going to communicate with event logger and log file which creates repudiation. 
- keep appending to a log file
- with every request, logger intercepts the request and gets infomration on it
    - sends it to the next end point depends on the request that was made
    - goes to error handling middleware if there is an error
    - tracks every request made to the services