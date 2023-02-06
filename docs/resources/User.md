# User resource

### User object

Represents a user.

###### User structure

| Field name            | Type                  | Description                                           |
| ---                   | ---                   | ---                                                   |
| id                    | snowflake             | The id of this user                                   |
| email                 | string                | The email linked to this user                         |
| first_name            | string                | The first name of the user                            |
| last_name             | string                | The last name of the user                             |
| verified              | boolean               | Whether the user has completed email verificiation    |
| password~             | string                | BCrypt hashed password                                |
| verification_token~   | string                | Token the user has to send along to verify            |


## Create new user % HTTP POST /user

###### Body parameters

| Field name            | Type                  | Description                                           |
| ---                   | ---                   | ---                                                   |
| email                 | string                | The email linked to this user                         |
| first_name            | string                | The first name of the user                            |
| last_name             | string                | The last name of the user                             |
| password              | string                | The unencrypted password for the user                 |

Returns a [user](/docs/resources/User.md#user-structure) object on success with a 201 status code.

## Verify user % HTTP GET /user/verify/:id/:token

Verifies the user, then on success redirects them to the homepage.

###### Query parameters

| Field name            | Type                  | Description                                           |
| ---                   | ---                   | ---                                                   |
| id                    | snowflake             | The id of this user                                   |
| verification_token    | string                | Token the user has to send along to verify            |

## Get current user % HTTP GET /user

Returns a [user](/docs/resources/User.md#user-structure) object on success with a 200 status code.
Returns a 401 if not authorized at the moment..

## Login to account % HTTP POST /user/login

###### Body parameters

| Field name            | Type                  | Description                                           |
| ---                   | ---                   | ---                                                   |
| email                 | string                | The email linked to this user                         |
| password              | string                | The unencrypted password for the user                 |

###### Return body parameters

| Field name            | Type                  | Description                                           |
| ---                   | ---                   | ---                                                   |
| access_token          | string                | The jwt access token of the user                      |
| refresh_token         | string                | The jwt refresh token of the user                     |

> **Note**
> The `access_token` jwt token contains the following fields: `id`, `email`, `verified`, `first_name`, `last_name`

> **Note**
> The `refresh_token` jwt token contains the following fields: `id`

## Refresh access token % HTTP POST /user/refresh

###### Body parameters

| Field name            | Type                  | Description                                           |
| ---                   | ---                   | ---                                                   |
| refresh_token         | string                | The jwt refresh token of the user                     |

###### Return body parameters

| Field name            | Type                  | Description                                           |
| ---                   | ---                   | ---                                                   |
| access_token          | string                | The jwt access token of the user                      |
| refresh_token         | string                | The jwt refresh token of the user                     |

> **Note**
> The `access_token` jwt token contains the following fields: `id`, `email`, `verified`, `first_name`, `last_name`

> **Note**
> The `refresh_token` jwt token contains the following fields: `id`