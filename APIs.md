# APIs for TSDB-Project

Backend APIs document for this project.

## Common

> To be editted, not in Mininum Prototype

All API URLs need to start with `/apis/`. Time supposed to be **UTC**.

## Patients

Path: `patients/` (eg. `http://127.0.0.1:8080/apis/patients/`)

| ID | Sub-path | Method | Role | Example URL |
|:---:|:---|:---:|:---|:---|
|1|/find|GET|Find all patients|`http://127.0.0.1:8080/apis/patients/find`|
|2|/find|POST|Find patients with certain criteria|`http://127.0.0.1:8080/apis/patients/find`|
|3|/{id}|GET|Find a patient with specific PID|`http://127.0.0.1:8080/apis/patients/PUH-2010-080`|

### Return vals

- Empty if no results
- Patient JSON array if there are multiple results
- Patient JSON object if one result

1. Examples (<http://127.0.0.1:8080/apis/patients/>):

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

2. Examples (<http://127.0.0.1:8080/apis/patients/PUH-2010-140>):

```json
{
    "imported_time": "2018-02-09T16:11:44.767Z",
    "pid": "PUH-2010-140",
    "age": 83,
    "gender": "F"
}
```


### Detailed params



## Query



## Files



## Export



## Import


