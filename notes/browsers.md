# Browsers

## Standardization
<details>
<summary>Learn more</summary>

- [TC39](https://tc39.es/)
- [TC39 - proposals](https://github.com/tc39/proposals)
- [WHATWG](https://whatwg.org/)
- [WHATWG - Standards](https://spec.whatwg.org/)
- [W3C](https://www.w3.org/TR/html52/)
- [W3C - CSS](https://www.w3.org/Style/CSS/)

</details>

## Browser engines
## The Internet
<details>
<summary>Basic process of publishing a website</summary>

1. Publish the website
  - Domain
    - check if it's free
    - domain registering service
    - sometimes need a passport to purchase
    - if there was ip in the dns settings, links to domain
  - Hosting
    - paid or free
    - gives an access to the server where the web server runs
    - gives a temporary address (site-name.hosting.com)
    - link the domain to the web server
    - deploy the website to hosting
2. Enter website name to the browser
3. Transfer the name to IP via [DNS](#dns)
4. Browser sends the HTTP request to the server (browserscope.org check the available amount of requests for different browsers)
  - [Transfer levels and protocols](#transfer-levels-and-protocols)
  - Doesn't know about server language
  - 1 file = 1 request (less weight and files = better)
  - contains of headers only
5. Gets to the physical server via cables
6. Looking for a program via port number (different for client and server): 80 or 443 (web server nginx, apache), on complete port closes
7. Web server could have several virtual hosts, get our by site name (domain)
8. Sending a response (headers and body: html, css, js, media, files)
9. Browser parses the code (according to the specification native to browser)

</details>

<details>
<summary>Learn more</summary>

- [ ] [How Websites Work](https://academind.com/learn/web-dev/how-the-web-works/)
- [How Browsers Work: Behind the scenes of modern web browsers](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)

</details>

## DNS
<details>
<summary>General info</summary>

- slow (up to 48 hours to update)
- large
- secure (complex implementation)
- distributed (uses cash)

</details>

## Transfer levels and protocols
<details>
<summary>Link layer</summary>

- cables

</details>

<details>
<summary>Internet layer</summary>

- IP (Internet Protocol) earlier IPv4, new IPv6
- describes the network structure and packets delivery system
- secure delivery is not guaranteed

</details>

<details>
<summary>Transport layer</summary>

- UTP - doesn't wait for the package to be delivered (sound, games, streams, video)
- TCP - waits for the packages (files, used by browsers)
  - lost or discarded packets are resent
  - includes traffic congestion control

</details>

<details>
<summary>Application layer</summary>

- HTTP(S) - HyperText Transfer Protocol (Secure)
- FTP - File Transfer Protocol
- SMTP - Simple Mail Transfer Protocol
- SSH - Secure Shell - for accessing remote servers (linux)

</details>

<details>
<summary>Learn more</summary>

- [Internet protocol suite](https://en.wikipedia.org/wiki/Internet_protocol_suite)

</details>

## Websites and deployment process
<details>
<summary>Types of websites</summary>

- Static (just HTML, CSS, JS)
- SPA (HTML, CSS, JS with only one HTML page being served, client-side JS is used to re-render the page dynamically)
- Dynamic (SSR) Web Apps (HTML pages are created dynamically on the server via template engines like EJS)

</details>

<details>
<summary>Deployment process</summary>

1. write the code
2. test the code
3. optimise the code
4. build for production
5. deploy depending on the type of website
  - static host - doesn't execute the server-side code: AWS S3, Firebase Hosting, etc
  - dynamic host - can execute the server-side code: AWS Elastic, Heroku, etc

</details>

<details>
<summary>Learn more</summary>

- [ ] [Dynamic vs Static vs SPA](https://academind.com/learn/web-dev/dynamic-vs-static-vs-spa/)
- [ ] [Firebase hosting docs](https://firebase.google.com/docs/hosting)
- [ ] [Heroku docs](https://devcenter.heroku.com/categories/reference)

</details>