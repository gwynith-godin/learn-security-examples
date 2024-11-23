# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

- in the existing form, we are accepting any inputs which are suppose to be plain strings. So we are allowing code injections.
- inputs are coming from the user which can come from any place
- valid code will be operated at runtime

2. Briefly explain how a malicious attacker can exploit them.

- a malicious user could insert a javascript script that deletes all the files form a database
3. Briefly explain why **secure.ts** does not have the same vulnerabilties?

- we want to sanitize all inputs- so make sure all inputs have the exact form that we expect it to be
