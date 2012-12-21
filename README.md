JSONPoo
=======

*Like JSONP, but better* 💩

## Synopsis

**JSONPoo** is a brand-new data format based on [JSONP](http://en.wikipedia.org/wiki/JSONP). It is here to solve all problems with JSONP. Although there are currently no problems, it is always a good idea to have yet another data format.

## Concept

Currently it is really annoying that you have to pass the funciton name via the url, like `http://server2.example.com/Users/1234?jsonp=parseResponse`. This seems like a dirty hack and is not state of the art.

JSONPoo specifies that all callbacks have to be done via the `💩`-property of the `window`-object. The function is called with the first parameter being the url of the requested resource. All other parameters are optional and depend on the resource.

Within the `💩`-callback you can separate the incoming data by the url and proceed with the received data.

## Example

Inject into the head of the document:

```html
<script type="text/javascript" src="http://server.example.com/users/1234"></script>
```

And the server will respond with:

```javascript
window["💩"]("http://server.example.com/users/1234", { name: "Hirsl", age: 25 });
```

Now all you have to do is to define:

```javascript
window["💩"] = function (url) {
    var args = Array.prototype.slice.call(arguments, 1);
    
    switch (url) {
        case "http://server.example.com/users/1234":
            addUser.apply(null, args);
            break;
        ...
    }
};
```

*Please note, that the 💩-symbol is currently not allowed to be used in JavaScript-code. Therefore you have to escape it with brackets. A proposal for standardization is on the way.*
