# Leaderboard API
The leaderboard APIs allow creators to make applications. Think of an application as game or title. Once you have an application you can then create leaderboards for your applications. The leaderboard API also allows players to create and get stats.

## Creator APIs
**NOTE** Remember that you will need a `creator` account and be logged in to get an access token to access the `CreateApplication` and `CreateLeaderboard` APIs. See the [UserAPI creator quick start](https://github.com/GameStackTech/GameStackDocs/blob/main/docs/UserAPIs.md#creator-quick-start) guide for info on how to signup for a creator account and how to login to get an access token.

### Create application
Applications represent your games or titles. An application is required to create leaderboards. To create an application you can use the following CURL example.

You will need to provide the following information in your call to the **/app** API.

* Headers
  * `Authorization`
    * Required: **Yes**
    * Value: `Bearer <your_access_token>`
    * Description: A valid access token for a GameStack creator.
* Body
  * `name`
    * Required: **Yes**
    * Data type: **string**
    * Description: The name of the application.

**Sample request**
```sh
curl -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"name":"DemoGame"}' http://localhost:8080/app
```

If successful you will get a response with you new applications ID. You will want to make a note of this as you will need if for calls to create leaderboards.

**Sample response**
```json
{"application_id":"7cb1fa38b8e15fb78fe2dc1984a24dbeb87cdc69"}
```

### Create leaderboard
Leaderboards contain player statistics. To make a leaderboard you need an application that the leaderboard will belong to. You can create a leaderboard using the following CURL example.

You will need to provide the following information in your call to the **/app/{applciation_id}/leaderboard** API.

* Headers
  * `Authorization`
    * Required: **Yes**
    * Value: `Bearer <your_access_token>`
    * Description: A valid access token for a GameStack creator.
* URL
  * `/app/{applciation_id}/leaderboard`
    * `application_id`
      * Required: **Yes**
      * Data type: **string**
      * Description: The ID of the applciation the leaderboard will belong to.
* Body
  * `name`
    * Required: **Yes**
    * Data type: **string**
    * Description: The name of the leaderboard.
  * `dimensions`
    * Required: **Yes**
    * Data type: **map[string]Dimension**
    * Description: A key/value lookup of diemnsion names to `Dimension` values. This is how you define the name of your stats and their data type.

**Sample request**
```sh
curl -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"name":"DemoLeaderboard","dimensions":{"wins":{"data":{"type":"INT"}},"losses":{"data":{"type":"INT"}}}}' http://localhost:8080/app/<your_applciation_id>/leaderboard
```

If successful you will get a response with your new leaderboards ID. You will want to make a note of this as you will need if for calls to put and get stats.

**Sample response**
```json
{"leaderboard_id":"leaderboard_5e4be46964896293a3f626d0304fg6cb37a35279"}
```

## Player APIs
**NOTE** Remember that you will need a `player` account and be logged in to get an access token to access the `PutLeaderboardStats` and `GetLeaderboardStats` APIs. See the [UserAPI player quick start](https://github.com/GameStackTech/GameStackDocs/blob/main/docs/UserAPIs.md#player-quick-start) guide for info on how to signup for a player account and how to login to get an access token.

You will also need to register your `player` account as a user of your application to access the `PutLeaderboardStats` API. See the **Create user** section below for more information.

### Create user
Each of a creators applications has users associated with it. By registering GameStack players as users with your application you can allow players to have a different alias per application if the want, or they can use their GameStack alias.

You will need to provide the following information in your call to the **/app/{application_id}/user** API.

* Headers
  * `Authorization`
    * Required: **Yes**
    * Value: `Bearer <your_access_token>`
    * Description: A valid access token for a GameStack player.
* URL
  * `app/{application_id}/user`
    * `application_id`
      * Required: **Yes**
      * Data type: **string**
      * Description: The ID of the applciation the GameStack player will be registered as a user of.
* HTTP Verb
  * **PUT**
* Body
  * `alias`
    * Required: **Yes**
    * Data type: **string**
    * Description: The alias the user wishes to register as for the applciation.

**Sample request**
```sh
curl -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"alias":"someAlias"}' -X PUT http://localhost:8080/app/<your_application_id>/user
```

**Sample response**
```json
{"id":"5cd148b9-5080-4c91-83eg-17f4ed36a622"}
```

### Put leaderboard stats
Player statistics are uploaded via the `PutLeaderboardStats` API after a player has completed an event in your game like the finish of a 1:1 match, after completion of a dungeon, clearing a level, etc. Only GameStack players who have registered as users with your applciation can put stats. See the **Create user** section above for more information on registering a GameStack player as a user of your application.

You will need to provide the following information in your call to the **app/{applciation_id}/leaderboard/{leaderboard_id}/stats** API.

* Headers
  * `Authorization`
    * Required: **Yes**
    * Value: `Bearer <your_access_token>`
    * Description: A valid access token for a GameStack player.
* URL
  * `app/{applciation_id}/leaderboard/{leaderboard_id}/stats`
    * `application_id`
      * Required: **Yes**
      * Data type: **string**
      * Description: The ID of the applciation the leaderboard will belong to.
    * `leaderboard_id`
      * Required: **Yes**
      * Data type: **string**
      * Description: The ID of the leaderboard the stats will belong to.
* HTTP Verb
  * **PUT**
* Body
  * `dimensions`
    * Required: **Yes**
    * Data type: **List of Dimensions**
    * Description: The statistical dimensions that will be assigned to the player for this play instance.

**Sample request**
```sh
curl -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"dimensions":[{"name":"wins","data":{"val":"1","type":"INT"}},{"name":"rushYards","data":{"val":"112","type":"INT"}},{"name":"passYards","data":{"val":"257","type":"INT"}},{"name":"completionPercentage","data":{"val":"0.83","type":"FLOAT"}}]}' -X PUT http://localhost:8080/app/<your_applciation_id>/leaderboard/<your_leaderboard_id>/stats
```

### Get leaderboard stats