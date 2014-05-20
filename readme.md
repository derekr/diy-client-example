![](http://dofr7nqq7emks.cloudfront.net/gra_splash.jpg)

# Getting Started w/ diy-client

[diy-client](https://github.com/diy/diy-client) is the official js client
for the DIY API. With it you can interact with DIY data such as maker
and skill info.

You can download the files for this guide
[here](https://github.com/derekr/diy-client-example/archive/master.zip).
Once you have the files just open `index.html` in a browser and check
[the console](https://diy.org/skills/frontenddev/challenges/1030/find-bugs-with-web-inspector)
for output.

# Initial Steps

Create a HTML document and reference the `diy.dist.js` file.

```html
<script type="text/javascript" charset="utf-8" src="diy.dist.js"></script>
```

Then call the `diyClient` function which returns another function you can use
to make requests to the DIY API.

```html
<script type="text/javascript">
    var diy = diyClient();
</script>
```

# Requests

Now that we have a `diy` function we can ask the API for some data… Let's try
`maker` data. A call to `diy` requires **2 arguments**: a route or `uri` as the first argument and
a `callback` function as the second argument.

```html
<script type="text/javascript">
    var diy = diyClient();

    diy('/makers/drk', function (err, body) {
        console.log(body.response);
    });
</script>
```

Now we're cookin'! :egg:

The `uri` in this case is the `/makers/:url` resource. You can replace `:url`
with any existing maker url like `/makers/astro` to get their DIY data.

The `callback` function will be called when the request to the DIY API is done.

All of the response data can be found in the `body.response` variable, but first
you'll want to make sure there wasn't an error while requesting.

So we can beef up the callback function to be a little more tolerant:

```js
diy('/makers/drk', function (err, body) {
    if (err) return alert('Error fetching maker data.');

    console.log(body.response);
});
```

If there is an error we `return` early and alert that an error occured.

If everything went ok `body.response` should contain an object literal that
looks like this:

```json
{
    "id": 32581,
    "stamp": "2013-01-03T12:56:15.000Z",
    "url": "drk",
    "nickname": "drk",
    "email": "d*****@m*.com",
    "type": {
        "moderator": true,
        "adult": false,
        "subscriber": false,
        "verified": true,
        "suspended": false
    },
    "avatar": {
        "id": 93,
        "icon": {
            "url": "https://d3hv8qdd474bjn.cloudfront.net/drk_icon.png",
            "mime": "image/jpeg",
            "width": 30,
            "height": 28
        },
        "small": {
            "url": "https://d3hv8qdd474bjn.cloudfront.net/drk_small.png",
            "mime": "image/jpeg",
            "width": 90,
            "height": 90
        },
        "medium": {
            "url": "https://d3hv8qdd474bjn.cloudfront.net/drk_medium.png",
            "mime": "image/jpeg",
            "width": 160,
            "height": 150
        },
        "large": {
            "url": "https://d3hv8qdd474bjn.cloudfront.net/drk_large.png",
            "mime": "image/jpeg",
            "width": 460,
            "height": 431
        }
    },
    "portfolio": {
        "bio": "I write stuff.",
        "foreground": "#ffffff",
        "background": "#ffd531"
    },
    "stats": {
        "projects": 53,
        "achievements": 27,
        "patches": 6,
        "following": 111,
        "followers": 1099
    }
}
```

By this point your HTML file should look close to the included
[index.html](https://github.com/derekr/diy-client-example/blob/master/index.html) file.

That is the most basic way to get data from the DIY API! Once
you have this down try and guess how to fetch some skill data. If you need
some help figuring out the skill `uri` check [docs.diy.org](http://docs.diy.org).

# More Requests

Coming soon!

* How to add data to the API
* How to authenticate so you can post project from the api
* Search!

# FAQ

**Why do I have to call a `diyClient()` function to get the other function named `diy`?**

The initial call to `diyClient` allows you to set a custom API `host` and `version`
number, but most of the time you just want the default `http://api.diy.org` and
current API version. This is more of a convenience for DIY internally as
it allows us to easily swap out versions of the API while tesitng.

**What kind of data can I play with?**

You can see all the different types of data in the DIY API here:
See [docs.diy.org](http://docs.diy.org).

**Is there another way to install `diy-client`?**

Yup! `diy-client` is available in [npm](https://www.npmjs.org/package/diy) and
can be installed by running:

```shell
npm install diy
```

`diy-client` works both on the server in Node and in browsers that support
[CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS).

In the browser you can bundle `diy-client` w/
[browserify](https://github.com/substack/node-browserify) or use the standalone
`diy.dist.js` file included here.
