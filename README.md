<p align="center">
  <img src="/color-wash-logo-vertical.png" width="320" alt="Colorwash Logo" />
</p>

# Customer Control

Customer Control is a module in the backend that provides API endpoints to allow playing of preprogrammed light shows on G&G ColorWash hardware. The API is protected by an API key. The module receives incoming requests (with API key), matches a show index to a preprogrammed show stored on the backend, then sends a request to the specified ColorWash device with the appropriate details. 

## Security

The endpoints in this module are publicly exposed, but guarded with an API key. This single key is used for all incoming requests to the Customer Control endpoints. The API key should be included as a header in the request as per outlined below:
```ts
  X-API-KEY: apiKey  // Use apiKey provided by G&G LED
```

## API

### Server URL

All requests should be sent to the server address below:
```ts
https://api.dashboard.colorwash.app
```

### Public -> Customer Control
`POST /customer-control/show/:deviceID`

Receives `CustomerControlDto`, matches provided index with preprogrammed show, then sends a request to the specified colorwash device (matched to `:deviceID`) to start the show with provided timeout. The show can be stopped with the stop command as shown below. 

deviceID:

This is a unique 16 character alphanumeric code that is assigned to each G&G ColorWash device during manufacturing. It is marked inside of the control box for the system and can be provided by G&G LED as needed. 

CustomerControlDto:
```ts
{
  showNumber: number,  // this is the index of the preprogrammed show - Consult G&G for a show number set configured for your system.
  timeout: number,     // positive integer. Number of seconds the show will run for. 
}
```

`GET /customer-control/stop/:deviceID`

Sends a request to stop show to the specified device (matched to `:deviceID`). 

DTO: `none`
