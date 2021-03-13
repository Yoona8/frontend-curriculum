# Optimizations

## Startup time
<details>
<summary>General info</summary>

- Browser side (server code is already loaded)
- How long does it takes to see the content on the screen?
- How long does it takes till the user is able to interact with the website?

</details>

<details>
<summary>What to optimize?</summary>

- bundle size
- number of http requests

</details>

<details>
<summary>Learn more</summary>

- [DevTools: Rendering Performance on Google](https://developers.google.com/web/fundamentals/performance/rendering)
- [DevTools: Performance Analysis Reference on Google](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference)

</details>

## Runtime performance
<details>
<summary>General info</summary>

- Both browser and server
- How smooth does the app run? (Freezes or lags?)
- How smooth do the animations play? (Visual lags?)
- Are there any memory leaks? (Is the page getting slower?)

</details>

<details>
<summary>What to optimize?</summary>

- code execution, DOM access (avoid unnecessary code execution, DOM interactions, repaints)
- memory leaks (slows down the app)
- find better code alternatives (ex: other method for iteration)
- micro-optimizations (very specific use-case, ex: data structures for frequent access or changes)

</details>

<details>
<summary>Learn more</summary>

- [DevTools: Fix Memory Problems on Google](https://developers.google.com/web/tools/chrome-devtools/memory-problems)
- [New Performance Features: Make Your Pages Faster](https://youtu.be/8k_DEeIZpIc)
- [x] [Your first performance budget with Lighthouse](https://bitsofco.de/your-first-performance-budget-with-lighthouse/)

</details>

## Mobile UI
<details>
<summary>Random things</summary>

- `-webkit-overflow-scrolling: touch;` scroll native to iPhone (not sure, read more)

</details>

## Content
<details>
<summary>Learn more</summary>

- [ ] [Optimizing Content Efficiency](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency)

</details>

## CSS
<details>
<summary>Sometimes empty blocks</summary>

- for blocks, which could be empty, add `:empty { display: none; }`

</details>

<details>
<summary>Animations</summary>

- `will-change` for animations, but don't use often

</details>

## Load optimizations
<details>
<summary>Link tag</summary>

- `<link rel="prefetch">` if needed

</details>

## Server side
<details>
<summary>Compression of assets</summary>

- zipping static assets (CSS, JS, images) before serving
- browsers know how to unzip such files and will automatically do it
- less data is sent from server => faster load time
- on Firebase, static assets are automatically compressed
- sometimes you have to configure it manually

</details>

<details>
<summary>Caching (both frontend and server)</summary>

- saving data or files for re-use
- can be done on different levels
- browser automatically caches files (e.g. JS files) based on the caching headers set by the serving host
- controlling headers on the server-side config allows you to control how browsers will cache files
- helps to avoid unnecessary data transfer
- make sure to deliver updates properly
- server-side caching is all about storing data you work with on the server (e.g. fetched from a database) such that multiple requests requesting the same data can get that cached data

</details>

<details>
<summary>HTTP/2.0</summary>

- latest version of the HTTP protocol
- unlike HTTP/1 allows "server push" (servers can push required assets actively to a client instead of waiting for the client to request them)

</details>

<details>
<summary>Learn more</summary>

- [Express.js compression](https://github.com/expressjs/compression)
- [ ] [Cache-Control on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)
- [ ] [Prevent unnecessary network requests with the HTTP Cache](https://web.dev/http-cache/)
- [ ] [Site Cache vs Browser Cache vs Server Cache: What’s the Difference?](https://wp-rocket.me/blog/different-types-of-caching/)
- [ ] [Introduction to HTTP/2](https://developers.google.com/web/fundamentals/performance/http2)

</details>

## Tools and resources
<details>
<summary>Measuring the performance</summary>

- [performance.now() API on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now)

</details>

<details>
<summary>Checklists</summary>

- [Service: The Front-End Checklist](https://frontendchecklist.io/) great checklist on what to check before deployment
- [Service: Checklist Design](https://www.checklist.design/) a collection of the best UX and UI practices

</details>