# Host

## Host informations

*Host informations* is a JSON data which specifies the details of the host.

### [WIP] Endpoint

It may provided with the path "/.well-known/yayaka".

### JSON format

A packet is an object have following properties.


- MUST **yayaka-version** semver  
  The version of Yayaka Protocol

- MUST **host-version** semver  
  The version of the specification of the host

- MUST **connection-protocols** object  
  An object which has following properties and uses the name of the connection protocol as a key

  - MUST **version** semver  
    The version of the connection protocol

  - MAY **parameters** object  
    The parameters for the connection protocol

- MUST **message-protocols** array  
  An object which has following properties and uses the name of the message protocol as a key
  An array of objects which have following properties

  - MUST **version** semver  
    The version of the message protocol

  - MUST **services** array  
    An array of services provided in the host

  - MAY **parameters** object  
    The parameters for the message protocol

### Example

```json
{
  "yayaka-version": "1.0.0",
  "host-version": "1.0.0",
  "connection-protocols": {
    "https-jwt": {
      "version": "1.0.0",
      "parameters": {
        "connect-path": "/connect",
        "authenticate-path": "/authenticate"
      }
    },
    "phoenix-channel": {
      "version": "1.0.0",
      "parameters": {
        "websocket-path": "/socket/websocket",
        "topic-template": "remotes:{{host}}"
      }
    }
  },
  "message-protocols": {
    "yayaka": {
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
    "status": {
      "version": "1.0.0",
      "services": ["monitor"]
    }
  }
}
```
