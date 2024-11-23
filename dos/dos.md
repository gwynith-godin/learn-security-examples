# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.
- This is a classic denial of service because we passed a string and id is a mongo id, which is a specific format. If the ID is not in that format, it will error out. 
2. Briefly explain how a malicious attacker can exploit them.
- Using the get service, which retrieves the id form the query. If an attacker were to craft an ID which ends up crashing findOne, the server will crash. 
- Craft an input and a few of them could crash the server using a Dos. 
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
- Proper error handling so we do not crash unexpectedly
- sanitize the input. check if the user input is sanitized and make sure it is the expected format (24-char alphanumeric string). We dont actually do this in in **secure.ts**.
- rate limiter - define a middlewear function that is going to check if the rate limit is appropriate- every ip can send one request every 5 seconds- limit the amount of requests you can send per ip address so even if they cause harm they cannot cause too much harm.