# Galateia Bluetooth JSON-RPC API Specification

[//]: # (TODO: view the spec link)

[//]: # (TODO: Stateless, indempotent?)

The Galateia JSON-RPC API Specification is a collection of methods that the 
pump implements and clients, i.e. Apps, can use to control the pump. 
This interface allows for log inspection (metrics) as well as downstream tooling 
(firmware upgrades) and provides the infrastructure to treat different Apps 
as modules that can be swapped at will.

## Building

The specification is split into multiple files to improve readability. It
can be compiled into a single document as follows:

```console
$ npm install
$ npm run build
Build successful.
```

This will output the file `openrpc.json` in the root of the project. This file
will have all schema `#ref`s resolved.

## Running

```console
$ npm run mock-server

> bp-api@0.0.0 mock-server
> open-rpc-mock-server

Adding Transport of the type HTTPTransport on port 3333
Server Started
```

[//]: # (TODO: ## Testing)

## RPC Errors

| Class No. | Class Name     | Error No. | Error Message                    | Error Description                                                                                     |
|-----------|----------------|-----------|----------------------------------|-------------------------------------------------------------------------------------------------------|
| 100       | _Communication | -32601    | "Method not Found"               | The method does not exist / is not available                                                          |
| 100       | _Communication | -32700    | "Parse error"                    | Invalid JSON was received by the server. An error occurred on the server while parsing the JSON text. |
| 100       | _Communication | -32600    | "Invalid Request"                | The JSON sent is not a valid Request object.                                                          |
| 100       | _Communication | -32602    | "Invalid params"                 | Invalid method parameter(s).                                                                          |
| 100       | _Communication | 4         | "Device Not Ready"               |                                                                                                       |
| 100       | _Communication | 6         | "Command parameter out of range" | TODO: do we need this? Could just define proper patterns and types                                    |
| 300       | _Sensors       | 1         | "Sensor Error"                   | Error with Sensor Communication                                                                       |
|           |                |           |                                  |                                                                                                       |
|           |                |           |                                  |                                                                                                       |

Error example:
```json
{
    "id": 1,
    "jsonrpc": "2.0",
    "error": {
        "code": -32602,
        "data": [
            {
                "paramIndex": "firmware",
                "expectedSchema": {
                    "type": "string"
                },
                "name": "ParameterValidationError",
                "message": "Expected param at key: firmware to match the json schema: {\n  \"type\": \"string\"\n}. The function received instead .The Validation errors: \n[{\"keyword\":\"type\",\"dataPath\":\"\",\"schemaPath\":\"#/type\",\"params\":{\"type\":\"string\"},\"message\":\"should be string\"}]"
            }
        ],
        "message": "Invalid params"
    }
}
```