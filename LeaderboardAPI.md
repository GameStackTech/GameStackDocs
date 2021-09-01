# Leaderboard API
The leaderboard APIs allow creators to make applications. Think of an application as single game or title. Once you have an application you can then create leaderboards for your applications. The leaderboard API also allows players to create and get stats.

**NOTE** Remember that you will need a creator account and be logged in to get an access token to access the `CreateApplication` and `CreateLeaderboard` APIs. See the [UserAPI creator quick start](https://github.com/GameStackTech/GameStackDocs/blob/main/UserAPI.md#creator-quick-start) guide for info on how to signup for a creator account and how to login to get an access token.

## Create application
To create an application you can use the following CURL example.

**Sample request**
```sh
curl -v -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"name":"DemoGame"}' http://localhost:8080/app
```

If successful you will get a response with you new applications ID. You will want to make a note of this as you will need if for calls to create leaderboards.

**Sample response**
```json
{"application_id":"7cb1fa38b8e15fb78fe2dc1984a24dbeb87cdc69"}
```