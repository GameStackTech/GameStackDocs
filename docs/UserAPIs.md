# User APIs
GameStack has 2 kinds of users.

**Creators**

Creators are the people that make the games.

**Players**

Players are the people that use the creators games.

GameStack user APIs allow creation and management of accounts for both creators and players as well as authentication. The following sections are quick start guides that will show you how to make creator and player accounts via the GameStack REST API and how to login and authenticate with you account(s).

## Creator quick start
### Signup
To start using GameStack in your games you need to make a creator account so you can make applications and leaderboards for those applications.

You will need to provide the following information in your call to the **/signup** API.

* Body
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

**Creator signup REST API example**

```sh
curl -H 'Content-Type: application/json' -d '{"email":"some@email.com","first_name":"ContactsFirstName","last_name":"ContactsLastName","organization":"ContactsOrganizationName","password":"test"}' http://localhost:8070/signup
```

### Authenticate
Once you have made your creator account you can now authenticate (I.E. login) to GameStack to get an access token which will allow you to make calls to protected GameStack APIs so you can create applications and leaderboards later on.

You will need to provide the following information in your call to the **/login** API.

* Body
  * `email`
    * Required: **Yes**
    * Data type: **string**
    * Description: The email of the creator account that you want to login with.
  * `password`
    * Required: **Yes**
    * Data type: **string**
    * Description: The password to access the creator account.

**Creator login REST API example**

```sh
curl -H 'Content-Type: application/json' -d '{"email":"some@email.com","password":"test"}' http://localhost:8070/login
```

## Player quick start
### Signup
GameStack players put and get stats from leaderboards. To create a GameStack player account you will need to supply the following information.

* Body
  * `username`
    * Required: **Yes**
    * Data type: **string**
    * Description: The players name. Must be unique among GameStack users.
  * `email`
    * Required: **Yes**
    * Data type: **string**
    * Description: The players email address.
  * `name`
    * Required: **No**
    * Data type: **string**
    * Description: The players real life name.
  * `password`
    * Required: **Yes**
    * Data type: **string**
    * Description: The password to access the players account.

**Player signup REST API example**
```sh
curl -H 'Content-Type: application/json' -d '{"username":"some_username","email":"some@email.com","name":"Some User","password":"test"}' http://localhost:8070/players/signup
```

### Authenticate
Once you have made a player account you can now authenticate (I.E. login) to GameStack to get an access token which will allow you to make calls to protected GameStack APIs so you can put to and get stats from leaderboards.

* Body
  * `username`
    * Required: **Yes**
    * Data type: **string**
    * Description: The players username.
  * `password`
    * Required: **Yes**
    * Data type: **string**
    * Description: The password to access the players account.

**Player login REST API example**
```sh
curl -H 'Content-Type: application/json' -d '{"username":"some_username","password":"test"}' http://localhost:8070/players/login
```