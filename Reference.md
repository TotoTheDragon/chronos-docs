# API Reference

###### Base URL

```
https://chronos.example.com/api
```

## Versioning

To allow for future changes to our API structure, while making sure we do not break any features, we make use of versioning for major changes. As of now the default version is `1`

###### Versions

| Version   | Status    | 
| ---       | ---       |
| 1         | WIP       |


## Snowflakes

We make use of a modified [Twitter's snowflake] format for IDs. These are unique across every object we have. They are returned as strings because some languages do not handle 64 bit integers well.

###### Epoch

We set our epoch around the time the project started. The 1st of December 2022.
Our epoch is `1669852800000`

###### Binary representation

```
11111111111111111111111111111111111111111111111 11111 111111111111
64                                              17    12          0
```

###### Format

| Field               | Bits     | Number of bits | Retrieval                            |
| ------------------- | -------- | -------------- |  ----------------------------------- |
| Timestamp           | 63 to 17 | 47 bits        |  `(snowflake >> 17) + 1669852800000` |
| Internal machine ID | 16 to 12 | 5 bits         |  `(snowflake & 0x1F000) >> 12`       |
| Sequence            | 11 to 0  | 12 bits        |  `snowflake & 0xFFF`                 |