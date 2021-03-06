# xhr-plus
---

XMLHttpRequest plus. support jsonp, iframe upload, sub domain proxy and more...

[![NPM version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]
[![Test coverage][coveralls-image]][coveralls-url]
[![gemnasium deps][gemnasium-image]][gemnasium-url]
[![npm download][download-image]][download-url]

[npm-image]: http://img.shields.io/npm/v/xhr-plus.svg?style=flat-square
[npm-url]: http://npmjs.org/package/xhr-plus
[travis-image]: https://img.shields.io/travis/yiminghe/xhr-plus.svg?style=flat-square
[travis-url]: https://travis-ci.org/yiminghe/xhr-plus
[coveralls-image]: https://img.shields.io/coveralls/yiminghe/xhr-plus.svg?style=flat-square
[coveralls-url]: https://coveralls.io/r/yiminghe/xhr-plus?branch=master
[gemnasium-image]: http://img.shields.io/gemnasium/yiminghe/xhr-plus.svg?style=flat-square
[gemnasium-url]: https://gemnasium.com/yiminghe/xhr-plus
[node-image]: https://img.shields.io/badge/node.js-%3E=_0.10-green.svg?style=flat-square
[node-url]: http://nodejs.org/download/
[download-image]: https://img.shields.io/npm/dm/xhr-plus.svg?style=flat-square
[download-url]: https://npmjs.org/package/xhr-plus

## Example

http://localhost:8000/examples/

## install

[![xhr-plus](https://nodei.co/npm/xhr-plus.png)](https://npmjs.org/package/xhr-plus)

## Usage

```js
import io from 'xhr-plus';
io({
 url: '//x.com',
 method: 'get',
 data: {
   param: 'v',
 },
 success(data) {
 },
 error(e) {
 },
}).then((data) => {

}).catch(e => {

});
```

Promise support, place the following code inside your html head

```html
<script>
  if(!window.Promise) {
    document.writeln('<script src="https://as.alipayobjects.com/g/component/es6-promise/3.2.2/es6-promise.min.js"'+'>'+'<'+'/'+'script>');
  }
</script>
```

## API

```js
var req = io(config);
// req.abort();
```

### config

<table class="table table-bordered table-striped">
    <thead>
    <tr>
        <th style="width: 100px;">name</th>
        <th style="width: 50px;">type</th>
        <th style="width: 50px;">default</th>
        <th>description</th>
    </tr>
    </thead>
    <tbody>
        <tr>
          <td>url</td>
          <td>String</td>
          <td></td>
          <td>url requested</td>
        </tr>
        <tr>
          <td>method</td>
          <td>String</td>
          <td>get</td>
          <td>request method</td>
        </tr>
        <tr>
          <td>type</td>
          <td>a string enum. `html`, `xml`, `json`, or `jsonp`.
          Default is inferred by response contentType</td>
          <td>get</td>
          <td>response data, type</td>
        </tr>
        <tr>
          <td>data</td>
          <td>object|string</td>
          <td></td>
          <td> entity body for `PATCH`, `POST` and `PUT` requests. Must be a query `String` or `JSON` object</td>
        </tr>
        <tr>
          <td>form</td>
          <td>HTMLElement</td>
          <td></td>
          <td>submit entire form without page refresh</td>
        </tr>
        <tr>
          <td>cache</td>
          <td>bool</td>
          <td>true</td>
          <td>whether add timestamp to url</td>
        </tr>
        <tr>
          <td>traditional</td>
          <td>bool</td>
          <td>false</td>
          <td>whether add [] to array data key (if false then add [])</td>
        </tr>
        <tr>
          <td>headers</td>
          <td>object</td>
          <td>{}</td>
          <td>additional request headers</td>
        </tr>
        <tr>
          <td>contentType</td>
          <td>string</td>
          <td></td>
          <td>sets the `Content-Type` of the request. Eg: `application/json`</td>
        </tr>
        <tr>
          <td>processData</td>
          <td>boolean</td>
          <td>true</td>
          <td>whether format data to string</td>
        </tr>
        <tr>
          <td>timeout</td>
          <td>number</td>
          <td></td>
          <td>timeout by seconds</td>
        </tr>
        <tr>
          <td>beforeSend</td>
          <td>(io) => void</td>
          <td></td>
          <td>A function called before the request</td>
        </tr>
        <tr>
          <td>success</td>
          <td>(data, status, io) => void</td>
          <td></td>
          <td>A function called when the request successfully completes</td>
        </tr>
        <tr>
          <td>error</td>
          <td>({message, status, xhr}) => void</td>
          <td>true</td>
          <td>A function called when the request successfully error</td>
        </tr>
        <tr>
          <td>complete</td>
          <td>(data, status, io) => void</td>
          <td></td>
          <td>A function called when the request completes</td>
        </tr>
        <tr>
          <td>jsonpCallback</td>
          <td>string</td>
          <td>callback</td>
          <td>specify the jsonp request query name</td>
        </tr>
        <tr>
          <td>jsonpCallbackName</td>
          <td>string</td>
          <td>random string</td>
          <td>Specify the callback function name for a `JSONP` request.
          This value will be used instead of the random (but recommended) name automatically generated by ajax.</td>
        </tr>
        <tr>
          <td>withCredentials</td>
          <td>bool</td>
          <td>false</td>
          <td>whether to set withCredentials</td>
        </tr>
        <tr>
          <td>useSubDomainProxy</td>
          <td>false|'auto'|'force'</td>
          <td>false</td>
          <td>
              whether use iframe proxy to request sub domain,
              note: 'auto' will only works in non-cors browser,
              set to 'force' to force cors browser use sub domain proxy
          </td>
        </tr>
        <tr>
          <td>subDomainProxyUrl</td>
          <td>string</td>
          <td>/proxy.htm</td>
          <td>sub domain iframe proxy url</td>
        </tr>
    </tbody>
</table>

### methods

#### abort():void

abort current request

### then(data): Promise

use data in promise

### catch(e:{message, status, xhr}): Promise

catch error in promise

### always(data|e)

always process in promise

### static methods

#### ajaxSetUp(config)

set the default config for all requests

#### interceptors

You can intercept requests or responses like axios.

```js
// Add a request interceptor
io.interceptors.request.use((config) => {
  // Do something before request is sent
  return config;
});

// Add a response interceptor
io.interceptors.response.use(function (response) {
    // Do something with response data
    return response;
}, function (error) {
    // Do something with response error
    return Promise.reject(error);
});
```

And what's fun is you can turn a response into error

```js
io.interceptors.response.use(function (response) {
    if(response.notLogin) {
        const error = new Error('not login');
        error.isSystemError = true;
        return Promise.reject(error);
    }
});
```

If you may need to remove an interceptor later you can.

```js
var myInterceptor = io.interceptors.request.use(function () {/*...*/});
io.interceptors.request.eject(myInterceptor);
```




## Test Case

```
npm test
npm run chrome-test
```

## Coverage

```
npm run coverage
```

open coverage/ dir

## License

xhr-plus is released under the MIT license.
