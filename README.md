This repository contains the data collected as part of the São Paulo School of Advanced Science on Smart Cities, 2017.
The raw data consists of location and _motion activity_ traces from several participants in the school. All participants have consented to have their data publicly available.
The data is stored as a list of JSON objects, with both data and metadata.

The data is also available through a public ipython notebook server.
http://50.19.181.11:9999/tree?

### Example of location data ###

```
    {
        "user_id": {
            "$uuid": "18f729d9838a4e8ab66c3a6aac2ecdb0"
        },
        "_id": {
            "$oid": "5977356dcb17471ac056245f"
        },
        "data": {
            "loc": {
                "type": "Point",
                "coordinates": [
                    -46.6480565,
                    -23.5655504
                ]
            },
            "fmt_time": "2017-07-25T08:17:36.059000-03:00",
            "altitude": 0,
            "ts": 1500981456.059,
            "longitude": -46.6480565,
            "filter": "time",
            "elapsedRealtimeNanos": 124813051000000,
            "local_dt": {
            ...
            },
            "latitude": -23.5655504,
            "heading": 0,
            "sensed_speed": 0,
            "accuracy": 500
        },
        "metadata": {
            "write_fmt_time": "2017-07-25T08:17:37.154000-03:00",
            "write_ts": 1500981457.154,
            "time_zone": "America/Sao_Paulo",
            "platform": "android",
            "write_local_dt": {
            ...
            },
            "key": "background/location",
            "read_ts": 0,
            "type": "sensor-data"
        }
    },
```

### Examples of motion activity data ###

```
    {
        "user_id": {
            "$uuid": "18f729d9838a4e8ab66c3a6aac2ecdb0"
        },
        "_id": {
            "$oid": "5977356dcb17471ac0562464"
        },
        "data": {
            "type": 0,
            "confidence": 46,
            "local_dt": {
            ...
            },
            "ts": 1500981522.963,
            "fmt_time": "2017-07-25T08:18:42.963000-03:00"
        },
        "metadata": {
            "write_fmt_time": "2017-07-25T08:18:42.963000-03:00",
            "write_ts": 1500981522.963,
            "time_zone": "America/Sao_Paulo",
            "platform": "android",
            "write_local_dt": {
            ...
            },
            "key": "background/motion_activity",
            "read_ts": 0,
            "type": "sensor-data"
        }
    },
```
