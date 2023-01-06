# Session resource

### Session object

Represents the time a user worked.

###### Session structure

| Field name            | Type                  | Description                                    |
| ---                   | ---                   | ---                                            |
| id                    | snowflake             | The id of this session.                        |
| user                  | snowflake             | The id of the user this session belongs to.    |
| shift                 | ?snowflake            | The id of the shift that this corresponds to.  |
| original_start_time   | ISO8601 timestamp     | The time the user clocked in.                  |
| original_end_time     | ?ISO8601 timestamp    | The time the user clocked out.                 |
| start_time            | ISO8601 timestamp     | The time the user is clocked in.               |
| end_time              | ?ISO8601 timestamp    | The time the user is clocked out.              |
| description           | string                | What was done during this session.             |

###### Example Session

```json
{
    // TODO Create example data
}
```


## Get sessions % HTTP GET /sessions

Returns an array of sessions for the authenticated user. 
Returns an array of [session](/docs/resources/Session.md#session-object) objects.

###### Query parameters

| Field     | Type      | Description                           | Default       |
| ---       | ---       | ---                                   | ---           |
| before?   | snowflake | Get all sessions before this ID       | absent        |
| after?    | snowflake | Get all sessions after this ID        | absent        |
| limit?    | integer   | The max amount of sessions to return  | 25            |

## Export sessions to file % HTTP GET /sessions/export

Returns an list of all the sessions within the specified time, the output will be in the specified format.
Returns a [file](/docs/Reference.md#file-formatting) according to the specified format.

###### Query parameters

| Field     | Type                                                  | Description                           | Default       |
| ---       | ---                                                   | ---                                   | ---           |
| format?   | [file format name](/docs/Reference.md#file-formats)   | The format you want the file in       | excel         |
| before?   | snowflake                                             | Get all sessions before this ID       | absent        |
| after?    | snowflake                                             | Get all sessions after this ID        | absent        |

## Create session % HTTP POST /sessions

Returns the newly created session. In case the user currently has a session that has not yet ended, we will send back a 409 Conflict. 
Returns a [session](/docs/resources/Session.md#session-object) object on success.

## Edit session % HTTP PATCH /sessions/{[session.id](/docs/resources/Session.md#session-object)}

Used to either update the session or to end a session. 
Can only edit `start_time` and `end_time` when the session has ended.
If the session already has `original_end_time` set, it cannot be changed anymore.
Returns a [session](/docs/resources/Session.md#session-object) on success.

###### JSON Params

| Field                 | Type                  | Description                                    |
| ---                   | ---                   | ---                                            |
| original_end_time?    | ISO8601 timestamp     | The time the user clocked in.                  |
| description?          | string                | What was done during the session.              |
| start_time?           | ISO8601 timestamp     | The time the user is clocked in.               |
| end_time?             | ?ISO8601 timestamp    | The time the user is clocked out.              |
