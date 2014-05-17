![](http://dofr7nqq7emks.cloudfront.net/gra_splash.jpg)

# Getting Started w/ diy-client

[`diy-client`](https://github.com/diy/diy-client) is the official js client
for the DIY API. With it you can fetch DIY data such as maker and skill info.
See [docs.diy.org](http://docs.diy.org) for all available resources.

`diy-client` works both on the server in Node and in browsers that support
[CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS).

In the browser you can bundle `diy-client` w/
[browserify](https://github.com/substack/node-browserify) or use the standalone
`diy.dist.js` file included here.

For simplicity I am explaining how to use the standalone version.

# Initial Steps

Create an HTML document and reference the `diy.dist.js` file.

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

The initial call to `diyClient` allows you to set a custom API `host` and `version`
number, but most of the time you just want the default `http://api.diy.org` and
current API version.

# Requests

Now that we have a `diy` function we can fetch something like maker data. A call
to `diy` requires a route or uri as the first argument and a callback function
as the second argument.

```html
<script type="text/javascript">
    var diy = diyClient();

    diy('/makers/drk', function (err, body) {
        console.log(body.response);
    });
</script>
```

Now we're cookin'! :egg:

The uri in this case is the `/makers/:url` resource. You can replace `:url`
with any existing maker url like `/makers/astro` to get their DIY data.

The callback function will be called when the request to the DIY API is done.

All the response data can be found in the `body.response` variable, but first
you'll want to make sure there wasn't an error while requesting.

So we can beef up the callback function to be a little more tolerant:

```js
diy('/makers/drk', function (err, body) {
    if (err) return alert('Error fetching maker data.');

    console.log(body.response);
});
```

If there is an error we `return` early and alert that an error occured.

That is the most basic way to fetch data from the DIY API! Once
you have this down try and guess how to fetch some skill data. If you need
some help figuring out the skill uri check [docs.diy.org](http://docs.diy.org).

# More Requests

Coming soon!

* How to add data to the API
* How to authenticate so you can post project from the api
* Search!
