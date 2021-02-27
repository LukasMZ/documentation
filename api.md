# API Specification

## Driver Endpoint

### POST /driver/start
Request Body
```json
{
    "locations": [
        {
            "latitude": "o",
            "longitude": "Float"
        }
    ],
    "seats": "int",
    "preferences": {
        "smoker": "Boolean",
        "children": "Boolean"
    }
}
```

Response
```json
{
    "sessionId": "String" 
}
```

### GET /driver/information
Header
```
Authorization: <sessionId>
```

Response
```json
{
    "passengerId": "UUID",
    "pickupPoint": {
        "latitude": "Float",
        "longitude": "Float"
    },
    "dropoffPoint": {
        "latitude": "Float",
        "longitude": "Float"
    },
    "requested": "Boolean"
}
```

### POST /driver/locations
Header
```
Authorization: <sessionId>
```
Request Body
```json
[
    {
        "latitude": "Float",
        "longitude": "Float"
    }
]
```
Response
```
200 OK
```

### POST /driver/estimations
Header
```
Authorization: <sessionId>
```
Request Body
```json
[
    {
        "passengerId": "UUID",
        "pickupTime": "Int",
        "destinationTime": "Int"
    }
]
```
Response
```
200 OK
```

### POST /driver/confirmations
Header
```
Authorization: <sessionId>
```
Request Body
```json
[
    {
        "passengerId": "UUID",
        "accepted": "Boolean"
    }
]
```
Response
```
200 OK
```

### POST /driver/pickup
Header
```
Authorization: <sessionId>
```
Request Body
```json
{
    "passengerId": "UUID"
}
```
Response
```
200 OK
```

## Passenger Endpoint
### POST /passenger/start
Request Body
```json
{
    "location": {
        "latitude": "Float",
        "longitude": "Float"
    },
    "destination": {
        "latitude": "Float",
        "longitude": "Float"
    },
    "tolerance": "Integer",
    "requestedSeats": "Integer",
    "preferences": {
        "smoker": "Boolean",
        "children": "Boolean"
    }
}
```
Response
```json
{
    "sessionId": "String"
}
```

### GET /passenger/information
Header
```
Authorization: <sessionId>
```
Request Body
```json
[
    {
        "driverId": "UUID",
        "pickupTime": "Int",
        "destinationTime": "Int"
    }
]
```
Response
```
200 OK
```

### POST /passenger/location
Header
```
Authorization: <sessionId>
```
Request Body
```json
{
    "latitude": "Float",
    "longitude": "Float"
}
```
Response
```
200 OK
```

### POST /passenger/request
Header
```
Authorization: <sessionId>
```
Request Body
```json
{
    "driverId": "UUID"
}
```
Response
```
200 OK
```