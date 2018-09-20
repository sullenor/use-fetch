# use-fetch

A thin `fetch` wrapper with useful defaults. Inspired by [got](https://github.com/sindresorhus/got).


## Installation

### from npm
```bash
npm install use-fetch
```
or
```bash
yarn add use-fetch
```

### from unpkg
```html
<script src="https://unpkg.com/use-fetch@0.0.1/dist/index.js"></script>
<script src="https://unpkg.com/use-fetch@0.0.1/dist/index.min.js"></script>
```

You can access package through `window.usefetch`.


## Usage
```js
import usefetch from 'use-fetch';

usefetch('/messages', { json: true })
  .then(response => {
    console.log(response.body);
  });
```

### API

#### usefetch(input, [init])
Returns a promise for a `response` object with a `body` property.

##### input
Type: `string` `object`

The URL to request as a string or a [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) object.

##### init
Type: `object`

Any of the [fetch init](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch#Parameters) options.

###### headers
Type: `object`<br>
Default: `{}`

Request headers.

###### json
Type: `boolean`
Default: `false`

If set to `true` and `content-type` header is not set, it will be set to `application/json`.

Takes a [response](https://developer.mozilla.org/en-US/docs/Web/API/Response) stream and reads it to completion through the `response.json()`. The result is parsed as JSON and saved to `response.body`. Sets the `accept` header to `application/json`.

`body` must be a plain object or array and will be stringified.

###### timeout
Type: `number`<br>
Default: `0`

Milliseconds to wait for the server to respond before aborting request with error. By Default there's no timeout.


### Advanced
To create `fetch` with your own preset use the `createFetch` function. By default it is initialized as in the example below.

```js
import { createFetch } from 'use-fetch';

const usefetch = createFetch({
  // spec
  credentials: 'same-origin',
  redirect: 'follow',
  // custom
  json: false,
  redirect: 'follow',
  throwHttpErrors: true,
  timeout: 0,
});

export default usefetch;
```


## Errors
Each error contains (if available) `status`, `statusText`, `url` and `response` properties to make debugging easier.

#### usefetch.HTTPError
When server response code is not 2xx.

#### usefetch.ParseError
When `json` option is enabled, server response code is 2xx, and `response.json()` fails.

#### usefetch.TimeoutError
When server didn't respond within specified timeout.


## Future plans
- Add support of [AbortController](http://devdocs.io/dom/abortcontroller) with request cancellation.
- Read response stream as text by default.
- Add support of the [Request](http://devdocs.io/dom/request) object.


## License
> The MIT License
