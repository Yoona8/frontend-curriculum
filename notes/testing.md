# Testing
<details>
<summary>Why?</summary>

- minimize errors
- save time
- thinking about possible issues and bugs
- integrate into build workflow
- break up complex dependencies
- improve the code

</details>

<details>
<summary>Kinds of tests</summary>

- unit tests
  - fully isolated (ex: testing one function)
  - write as much as possible
- integration tests
  - with dependencies (ex: testing a function that call another function)
  - a bunch of tests
- end-to-end (e2e) tests
  - full flow (ex: user flow through some feature)
  - a few of tests

</details>

<details>
<summary>Testing setup</summary>

- test runner
  - for all kinds
  - execute the tests and summarize the result
  - Mocha, Jest, etc
- assertion library
  - for all kinds
  - define testing logic, conditions
  - Chai, Jest, etc
- headless browser
  - mostly e2e
  - simulates browser interactions
  - Puppeteer, etc

</details>

<details>
<summary>Learn more</summary>

- [ ] [JS testing introduction](https://academind.com/learn/javascript/javascript-testing-introduction/)
- [ ] [Stubs, Spies and Mocks in JavaScript](https://www.harrymt.com/blog/2018/04/11/stubs-spies-and-mocks-in-js.html)
- [Jest](https://jestjs.io/docs/en/getting-started)

</details>