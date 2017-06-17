# Host

## Host informations

*Host informations* is a JSON data which specifies the details of the host.

### [WIP] Endpoint

It may provided with the path ".ymp" or "/.well-known/ymp".

### JSON format

A packet is an object have following properties.


- MUST **ymp-version** semver  
  The version of YMP

- MUST **connection-protocols** array  
  An array of objects which have following properties
  Same connection protocols with different versions are allowed.

  - MUST **name** string  
    The name of the connection protocol

  - MUST **version** semver  
    The version of the connection protocol

  - MAY **parameters** object  
    The parameters for the connection protocol

- MUST **service-protocols** array  
  An array of objects which have following properties
  Same service protocols with different versions are allowed.

  - MUST **name** string  
    The name of the connection protocol

  - MUST **version** semver  
    The version of the service protocol

  - MUST **services** array  
    An array of services provided in the host

  - MAY **parameters** object  
    The parameters for the service protocol

### Example

```json
{
  "yayaka-version": "1.0.0",
  "connection-protocols": [
    {
      "name": "https-jwt",
      "version": "1.0.0",
      "parameters": {
        "connect-path": "/connect",
        "authenticate-path": "/authenticate"
      }
    },
    {
      "name": "phoenix-channel",
      "version": "1.0.0",
      "parameters": {
        "websocket-path": "/socket/websocket",
        "topic-template": "remotes:{{host}}"
      }
    }
  ],
  "service-protocols": [
    {
      "name": "yayaka",
      "version": "1.0.0",
      "services": ["identity", "repository", "social-graph"],
      "parameters": {
        "presentation-protocols": {
          "github-flavored-markdown": {
            "version": "1.0.0"
          }
        }
      }
    },
    {
      "name": "status",
      "version": "1.0.0",
      "services": ["monitor"]
    }
  ]
}
```
