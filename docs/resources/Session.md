# Session resource

### Session object

Represents the time a user worked.

###### Session structure

| Field name            | Type                  | Description                                    |
| ---                   | ---                   | ---                                            |
| id                    | snowflake             | The id of this session.                        |
| shift                 | ?snowflake            | The id of the shift that this corresponds to.  |
| user                  | ?snowflake            | The id of the user this session belongs to.    |
| original_start_time   | ISO8601 timestamp     | The time the user clocked in.                  |
| original_end_time     | ?ISO8601 timestamp    | The time the user clocked out.                 |
| start_time            | ISO8601 timestamp     | The time the user is clocked in.               |
| end_time              | ?ISO8601 timestamp    | The time the user is clocked out.              |


###### Example Session

```json
{
    // TODO Create example data
}
```