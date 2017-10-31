This repository contains the data collected as part of the São Paulo School of Advanced Science on Smart Cities, 2017.

## Overview of data ##
The raw data consists of mobility traces from several participants in the school. All participants have consented to have their data publicly available. The data is stored as a list of JSON objects - each object contains both data and metadata.

### Types of data ###
The traces contain both raw data, and the results of some post-processing performed by the code at https://github.com/e-mission/e-mission-server. The raw data is untouched - the analysis results are stored as separate objects that represent views over the raw data. The raw location traces can be noisy and intermittent, but the post-processing also generates a stream of resampled data for easier use.

The post-processing is reasonably good, so the analysed trip and section data can be used directly, or researchers can choose to use the raw data and perform their own post-processing. If their post-processing is more accurate than the current one, they are encouraged to submit their work to the e-mission project (https://github.com/e-mission/e-mission-server)

A complete list of the raw data types, in order of general interest, is:
- `background/location`: location
- `background/filtered_location`: filtered_location
- `background/motion_activity`: motion_activity
- `manual/incident`: smiley or frownie incident reported by the user
- `background/battery`: battery level of the phone
- `stats/client_nav_event`: client navigation activity
- `stats/client_time`: response time on the client
- `stats/client_error`: error detected on the server
- `stats/pipeline_time`: run time for the pipeline on the server
- `stats/server_api_time`: response time on the server
- `statemachine/transition`: transitions for the state machine running on the phone

A complete list of the processed data types, in order of general interest, is:
- `analysis/cleaned_place`: a place that the user was at
- `analysis/cleaned_trip`: a trip between two places
- `analysis/cleaned_section`: a part of a trip that is in a particular mode - e.g. a walk -> bus -> walk trip has 3 sections
- `analysis/cleaned_stop`: a transition point between sections
- `analysis/cleaned_untracked`: time when the tracking was turned off (e.g. phone was turned off)
- `analysis/recreated_location`: location data after jumps have been removed, and resampled at a constant rate
- `segmentation/*`: objects similar to the ones above, created at an intermediate step in the pipeline


### Quick start ###

<del>
Public server has been shut down to save compute resources. Please let shankari@eecs.berkeley.edu know 
if you need this, and she can turn it back on.
</del>

Public server has been turned on, and will be turned off after some exploratory
work through the end of the year.

The data is also available through a public ipython notebook server at
http://54.242.190.228:9999/tree?
The password for the server is the organization that this repository is stored under (int.......)
The sample notebook below has examples of how to access all these objects and plot them on a map.
**NOTE: Please don't edit the notebook directly - this is a shared server.**
Make a copy of the notebook, label it with your name, and explore the data there.
http://50.19.181.11:9999/notebooks/Sample/Timeseries_Sample.ipynb

### Data format examples ###
Here are some simple examples of different types of collected data, both raw and processed.
This is not exhaustive, please explore the data to find other examples.

#### Location data ####

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

#### Motion activity data ####

```
    {
        "user_id": {
            "$uuid": "18f729d9838a4e8ab66c3a6aac2ecdb0"
        },
        "_id": {
            "$oid": "5977356dcb17471ac0562464"
        },
        "data": {
            "type": 0, # type mapping is defined at https://github.com/e-mission/e-mission-server/blob/master/emission/core/wrapper/motionactivity.py#L5
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

#### Cleaned trip ####

```
    {
        "user_id": {
            "$uuid": "18f729d9838a4e8ab66c3a6aac2ecdb0"
        },
        "_id": {
            "$oid": "59780c0388f6630e9e15fb53"
        },
        "data": {
            "distance": 5150.3710045199505,
            "end_place": {
                "$oid": "59780c0888f6630e9e15fcc7"
            },
            "raw_trip": {
                "$oid": "59780bfe88f6630e9e15fb14"
            },
            "start_loc": {
                "type": "Point",
                "coordinates": [
                    -46.662591,
                    -23.5562993
                ]
            },
            "end_ts": 1500982957,
            "start_ts": 1500981642.177,
            "start_fmt_time": "2017-07-25T08:20:42.177000-03:00",
            "end_loc": {
                "type": "Point",
                "coordinates": [
                    -46.7091967,
                    -23.57178
                ]
            },
            "source": "DwellSegmentationTimeFilter",
            "start_place": {
                "$oid": "59780c0888f6630e9e15fcc6"
            },
            "end_fmt_time": "2017-07-25T08:42:37-03:00",
            "end_local_dt": {...},
            "duration": 1314.8229999542236,
            "start_local_dt": {...}
        },
        "metadata": {
            "write_fmt_time": "2017-07-25T20:26:59.007203-07:00",
            "write_ts": 1501039619.007203,
            "time_zone": "America/Los_Angeles",
            "platform": "server",
            ....
            "key": "analysis/cleaned_trip"
        }
    },
```

#### Cleaned section ####

```
    {
        "user_id": {
            "$uuid": "18f729d9838a4e8ab66c3a6aac2ecdb0"
        },
        "_id": {
            "$oid": "59780c0388f6630e9e15fb5b"
        },
        "data": {
            "distances": [
                0.0,
                59.09202714889158,
                34.17619592486318,
                27.72127007665632,
                53.23523225567902,
                7.583539411079733,
                4.904789652679724,
                0.16229358259470306
            ],
            "distance": 186.87534805244425,
            "start_loc": {
                "type": "Point",
                "coordinates": [
                    -46.70812,
                    -23.5720217
                ]
            },
            "end_ts": 1500982957,
            "start_ts": 1500982776,
            "start_fmt_time": "2017-07-25T08:39:36-03:00",
            "end_loc": {
                "type": "Point",
                "coordinates": [
                    -46.7091967,
                    -23.57178
                ]
            },
            "sensed_mode": 2,
            "source": "SmoothedHighConfidenceMotion",
            "end_fmt_time": "2017-07-25T08:42:37-03:00",
            "end_local_dt": {...},
            "duration": 181,
            "start_stop": {
                "$oid": "59780c0388f6630e9e15fb64"
            },
            "trip_id": {
                "$oid": "59780c0388f6630e9e15fb53"
            },
            "start_local_dt": {...},
            "speeds": [
                0.0,
                1.969734238296386,
                1.1392065308287727,
                0.924042335888544,
                1.7745077418559674,
                0.2527846470359911,
                0.16349298842265744,
                0.16229358259470306
            ]
        },
        "metadata": {
            "write_fmt_time": "2017-07-25T20:26:59.207442-07:00",
            "write_ts": 1501039619.207442,
            "time_zone": "America/Los_Angeles",
            "platform": "server",
            "write_local_dt": {...},
            "key": "analysis/cleaned_section"
        }
    },
```
