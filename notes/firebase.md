# Firebase
<details>
<summary>Basic setup</summary>

- firebase.google.com
- console.firebase.com
- add project, default settings
- navigate to database => realtime database => create database
- choose start in test mode (when your auth functional is not ready yet)
- URL in the head is where to send a request
- to simulate errors change some rules to false (database => rules)

</details>

<details>
<summary>Authentication</summary>

- database => rules
- set the rule you need to `auth != null`
- authentication => set up sign-in method
- choose email/password => enable only top switch
- users tab - all the users
- find docs on Auth REST API

</details>

<details>
<summary>Learn more</summary>

- [Authenticate REST Requests](https://firebase.google.com/docs/database/rest/auth)

</details>