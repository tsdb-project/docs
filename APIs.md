# APIs for TSDB-Project

Backend APIs document for this project.

## Common

> To be editted, not in Mininum Prototype

All API URLs need to start with `/apis/`. Time is **UTC** in InfluxDB. All POST should be `application/x-www-form-urlencoded` unless noted.

## Patients

> Status: Backend on-going.

Path: `patients/` (eg. `http://127.0.0.1:8080/apis/patients/`)

| ID | Sub-path | Method | Role | Example URL |
|:---:|:---|:---:|:---|:---|
|1|/find|GET|Find all patients|`http://127.0.0.1:8080/apis/patients/find`|
|2|/find|POST|Find patients with certain criteria|`http://127.0.0.1:8080/apis/patients/find`|
|3|/{id}|GET|Find a patient with specific PID|`http://127.0.0.1:8080/apis/patients/PUH-2010-080`|

### Return vals

- Empty if no results.
- Patient JSON array if there are multiple results.
- Patient JSON object if **find by PID**.

### Detailed params

#### For id=2

Only has POST params:

| Key | Value | Example Value | isMandatory | Role | Notes |
|:---|:---|:---|:---|:---|:---|
| pid | String | "PUH-2010-014" | No | Find by PID | Overides other criteria |
| gender | String | "M" or "F" | No | Find by gender| Can be combined with other |
| minage | Integer | eg. 15 | No | Find by min age | Working `maxage` would turn into a age range search |
| maxage | Integer | eg. 50 | No | Find by max age | Working `minage` would turn into a age range search |

### Examples

- <http://127.0.0.1:8080/apis/patients/find>:

```json
[
    {
        "imported_time": "2018-02-09T11:05:05.870Z",
        "pid": "PUH-2010-014",
        "age": 67,
        "gender": "F"
    },
    ...
    {
        "imported_time": "2018-02-09T16:53:43.116Z",
        "pid": "PUH-2010-141",
        "age": 75,
        "gender": "M"
    }
]
```

- <http://127.0.0.1:8080/apis/patients/PUH-2010-140>:

```json
{
    "imported_time": "2018-02-09T16:11:44.767Z",
    "pid": "PUH-2010-140",
    "age": 83,
    "gender": "F"
}
```

## Query



## Files



## Export



## Import

> Status: Backend finished, need for info.

## TODOs

- [ ] Wrap result with a status class.
- [ ] Ask John for more details on AR/NoAR.
