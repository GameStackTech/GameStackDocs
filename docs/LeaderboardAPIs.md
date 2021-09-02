# Leaderboard API
The leaderboard APIs allow creators to make applications. Think of an application as single game or title. Once you have an application you can then create leaderboards for your applications. The leaderboard API also allows players to create and get stats.

**NOTE** Remember that you will need a creator account and be logged in to get an access token to access the `CreateApplication` and `CreateLeaderboard` APIs. See the [UserAPI creator quick start](https://github.com/GameStackTech/GameStackDocs/blob/main/docs/UserAPIs.md#creator-quick-start) guide for info on how to signup for a creator account and how to login to get an access token.

## Create application
Applications represent your games or titles. An application is required to create leaderboards. To create an application you can use the following CURL example.

You will need to provide the following information in your call to the **/app** API.

* Body
  * `name`
    * Required: **Yes**
    * Data type: **string**
    * Description: The name of the application.

**Sample request**
```sh
curl -v -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"name":"DemoGame"}' http://localhost:8080/app
```

If successful you will get a response with you new applications ID. You will want to make a note of this as you will need if for calls to create leaderboards.

**Sample response**
```json
{"application_id":"7cb1fa38b8e15fb78fe2dc1984a24dbeb87cdc69"}
```

## Create leaderboard
Leaderboards contain player statistics. To make a leaderboard you need an application that the leaderboard will belong to. You can create a leaderboard using the following CURL example.

You will need to provide the following information in your call to the **/app/{applciation_id}/leaderboard** API.

* URL
  * `/app/{applciation_id}/leaderboard*`
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

If successful you will get a response with you new leaderboards ID. You will want to make a note of this as you will need if for calls to put and get stats.

**Sample response**
```json
{"leaderboard_id":"leaderboard_5e4be46964896293a3f626d0304fg6cb37a35279"}
```