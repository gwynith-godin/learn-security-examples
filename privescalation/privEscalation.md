# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
- There is an implementation weaknesses - for example access control has a bug which results in elevation of privilege
- There is no check when the user enters a 
2. Briefly explain how a malicious attacker can exploit them.
- Privilege of escalation could happen when an attacker tries out different IDs 
- userID and newRole are coming from untrusted sources req.body
- will elevate the privileges of every userId even if a user is unauthorized
- there is no authentication wehn requiring a user to enter a privilege
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
- configure a session middleware to create authenication for every incoming request
- Session using htmlOnly=True so that the cookie is inaccessible programmically.
- also set sameSite=strict so that the browsers wont include any cross-site requests
- we know the user is authenicated by reading from req.session which is trusted.
- there is a problem with this implementation: 
    - secret is used to hash the random session id that gets generated
    - if the secret key is uploaded somewhere, the hacker can see it. secret key should not be hardcoded in the source code.
