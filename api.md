# API Specification

## Driver Endpoint

### POST /driver/start
Request Body
```json
{
    "locations": [
        {
            "latitude": "Coordinate",
            "longitude": "Coordinate"
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
    "userId": "UUID",
    "pickupPoint": {
        "latitude": "Coordinate",
        "longitude": "Coordinate"
    },
    "dropoffPoint": {
        "latitude": "Coordinate",
        "longitude": "Coordinate"
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
        "latitude": "Coordinate",
        "longitude": "Coordinate"
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
        "userId": "UUID",
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
        "userId": "UUID",
        "status": "accepted|declined"
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
    "userId": "UUID"
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
        "latitude": "Coordinate",
        "longitude": "Coordinate"
    },
    "destination": {
        "latitude": "Coordinate",
        "longitude": "Coordinate"
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
    "latitude": "Coordinate",
    "longitude": "Coordinate"
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