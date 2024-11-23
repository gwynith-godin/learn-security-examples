# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.

- If the session is set, then we assume that the user is authenticated
- With every subsequent request, cookies get sent to the server so it can remember the user
- The session management is insecure because the cookie can be read programatically, so a malicious user can access the cookie.


2. Briefly explain different ways in which vulnerability can be exploited.

- Server might not know where the HTTP request came from
- taking an authentication token and storing it as a cookie
- Because of the HTTP protocol, the cookie will reamin the same with every request once the user has authenticated the token, so this makes us vulnerable to session hijacking
- Any malicious user with access to the token can carry out a spoofing attack, regardless of if they know the users credentials or not. They can access this token by:
    - programatically reading the cookie
    - trick user into sending a fake request to itself then to the server
    - CSRF attacks

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
- setting the cookie httpOnly to true and sameSite to true
- prevents other domains from sending a request to the server
- prevents cookie stealing and CSRF