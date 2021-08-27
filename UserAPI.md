# User APIs
GameStack has 2 kinds of users.

**Creators**

Creators are the people that make the games.

**Players**

Players are the people that use the creators games.

GameStack user APIs allow creation and management of accounts for both creators and players as well as authentication. The following sections are quick start guides that will show you how to make creator and player accounts via the GameStack REST API and how to login and authenticate with you account(s).

## Creator quick start
### Signup
To start using GameStack for you games you need to make a creator account so you can make applications and leaderboards for those appications.

You will need to provide the following information in your call to the **/signup** API.

* `email`
  * Required: **Yes**
  * Data type: **string**
  * Description: The email that will be used to access the account.
* `first_name`
  * Required: **Yes**
  * Data type: **string**
  * Description: The given name of the owner contact for the account.
* `last_name`
  * Required: **Yes**
  * Data type: **string**
  * Description: The family name of the owner contact for the account.
* `organization`
  * Required: **Yes**
  * Data type: **string**
  * Description: The name of the organization that owns this account.
* `password`
  * Required: **Yes**
  * Data type: **string**
  * Description: The password for the account.
    * **Requirements**: The password needs to be encoded before it is used in the **/signup** API call. First the password needs to be converted into a **SHA512** hash. The **SHA512** hash then needs to be Hex encoded. Note that the resulting string needs to use **lower case** letters.
      * Example: The password **test** encodes to **ee26b0dd4af7e749aa1a8ee3c10ae9923f618980772e473f8819a5d4940e0db27ac185f8a0e1d5f84f88bc887fd67b143732c304cc5fa9ad8e6f57f50028a8ff**

**Creator signup REST API example**

```sh
curl -v -H 'Content-Type: application/json' -d '{"email":"some@email.com","first_name":"ContactsFirstName","last_name":"ContactsLastName","organization":"ContactsOrganizationName","password":"ee26b0dd4af7e749aa1a8ee3c10ae9923f618980772e473f8819a5d4940e0db27ac185f8a0e1d5f84f88bc887fd67b143732c304cc5fa9ad8e6f57f50028a8ff"}' http://localhost:8070/signup
```

### Authenticate
Once you have made your creator account you can now authenticate (I.E. login) to GameStack to get an access token which will allow you to make calls to protected GameStack APIs so you can create applications and leaderboards later on.

You will need to provide the following information in your call to the **/login** API.

* `email`
  * Required: **Yes**
  * Data type: **string**
  * Description: The email of the creator account that you want to login with.
* `password`
  * Required: **Yes**
  * Data type: **string**
  * Description: The password to access the creator account.
    * **Requirements**: The password needs to be encoded before it is used in the **/login** API call. First the password needs to be converted into a **SHA512** hash. The **SHA512** hash then needs to be Hex encoded. Note that the resulting string needs to use **lower case** letters.
      * Example: The password **test** encodes to **ee26b0dd4af7e749aa1a8ee3c10ae9923f618980772e473f8819a5d4940e0db27ac185f8a0e1d5f84f88bc887fd67b143732c304cc5fa9ad8e6f57f50028a8ff**

**Creator login REST API example**

```sh
curl -v -H 'Content-Type: application/json' -d '{"email":"some@email.com","password":"ee26b0dd4af7e749aa1a8ee3c10ae9923f618980772e473f8819a5d4940e0db27ac185f8a0e1d5f84f88bc887fd67b143732c304cc5fa9ad8e6f57f50028a8ff"}' http://localhost:8070/login
```

## Player quick start