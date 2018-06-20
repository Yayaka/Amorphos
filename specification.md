# Amorphos Protocol
Version: 0.1.0

## Introduction
Amorphos protocol is a messaging protocol for horizontally and vertically distributed web applications.
It focuses on minimum specification and higher extensibility.

## Terminology
<dl>
<dt>Host
<dd>
A <i>host</i> is a server which has unique hostname and implements Amorphos protocol.
</dd>

<dt>Service
<dd>
A <i>service</i> is a set of related functions.
They can be united on a same host and also be distributed into multiple hosts.
</dd>
</dl>

## Encoding
Amorphos uses JSON format with UTF-8 encoding.

## Host
### Host informations
*Host informations* is a JSON data which specifies the details of the host.

#### Endpoint
`https://HOSTNAME/.amorphos`

#### JSON format
##### Properties
A packet is an object have the following properties.

- **amorphos-version** semver REQUIRED 
  The version of Amorphos

- **connection-protocols** array REQUIRED
  An array of objects which have the following properties
  Same connection protocols with different versions are allowed.

  - **name** string REQUIRED
    The name of the connection protocol

  - **version** semver REQUIRED
    The version of the connection protocol

  - **parameters** object OPTIONAL
    The parameters for the connection protocol

- **service-protocols** array REQUIRED
    array of objects which have the following properties
    Same service protocols with different versions are allowed.

  - **name** string REQUIRED
    The name of the connection protocol

  - **version** semver REQUIRED
    The version of the service protocol

  - **services** array REQUIRED
    An array of services provided in the host

  - **parameters** object OPTIONAL
    The parameters for the service protocol

##### Example
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

## Connection
Each host must establish a *connection* first to communicate between two different hosts and transmit packets under the connection.
Amorphos doesn't specify the details of how to do that and each connection protocols do.

### Creating a connection
To create a connection between two hosts, any common connection protocol which is specified in the each host information can be used.
Hosts can ignore connections which aren't specified in their host informations.

### Sender validation
The connection layer MUST validate the sender property of a message by checking the host.

## Packet
A *packet* is a JSON data transferred between two different hosts under a connection.
It includes any number of messages.

### JSON format
#### Properties
A packet is an object have the following property
and SHOULD NOT have all other properties.

- **messages** array REQUIRED
  An array of messages

- SHOULD NOT all other properties

#### Example
```json
{
  "messages": [
    {
      "sender": {
        "host": "host1.example.com",
        "protocol": "example",
        "service": "form"
      },
      "id": "0123456789",
      "host": "host2.example.com",
      "protocol": "example",
      "service": "repository",
      "action": "post example",
      "payload": {
        "text": "example text"
      }
    }
  ]
}
```

## Message

A *message* is a JSON data transfered between two services.
It is transferred by a packet if the two services are on different hosts.


### Types of messages

There are two types of messages, request messages and answer messages.
Request messages is a basic type of messages and answer messages is a type for replying to a message.


### Layered message routing

Each request messages have the properties to routing, **host**, **protocol**, **service**, and **action**.
They are sent to proper message handlers by the following procedure.

1. A connection sends a messages to the specified **host**.
2. The **host** routes the message to the specified **protocol**.
3. The **protocol** routes the message to the specified **service**.
4. The **service** routes the message to the handler to handle the specified **action**.

Each answer messages have the properties to routing, **host**, **reply_to**.
They are sent to proper message callers by the following procedure.

1. A connection sends a messages to the specified **host**.
2. The **host** routes the message to the caller of a message which has specified "id".


### Validation

Each layers of message routing SHOULD check messages are addressed to themselves.
They also MAY ignore messages at any time if one or more of **host**, **protocol**, **service**, and **action** are unknown.


### Timeout

Amorphos doesn't specify about timeout of messages.
It's specified in a service protocol.


### Request Messages JSON format
#### Properties
A request message have following properties
and SHOULD NOT all other properties

- **sender** object REQUIRED
  An object which has following properties

  - **host** string REQUIRED
    A sender host

  - **protocol** string REQUIRED
    A sender protocol

  - **service** string REQUIRED
    A sender service

- **id** string REQUIRED
  An ID which is unique in sender host

- **host** string REQUIRED
  A destination host

- **protocol** string REQUIRED
  A destination protocol

- **service** string REQUIRED
  A destination service

- **action** string REQUIRED
  A destination action

- **payload** object REQUIRED
  The body of the message

#### Example
```json
{
  "sender": {
    "host": "host1.example.com",
    "protocol": "example",
    "service": "form"
  },
  "id": "0123456789",
  "host": "host2.example.com",
  "protocol": "example",
  "service": "repository",
  "action": "post example",
  "payload": {
    "text": "example text"
  }
}
```

### Answer Messages JSON Format
#### Properties
Difference of answer messages from request messages are they have **reply-to** property.
A answer message have following properties
and SHOULD NOT all other properties

- **sender** object REQUIRED
  An object which has following properties

  - **host** string REQUIRED
    A sender host

  - **protocol** string REQUIRED
    A sender service protocol

  - **service** string REQUIRED
    A sender service

- **id** string REQUIRED
  An ID which is unique in sender host

- **reply-to** string REQUIRED
  An ID of a message to reply

- **host** string REQUIRED
  A destination host

- **protocol** string REQUIRED
  A destination service protocol

- **service** string REQUIRED
  A destination service

- **action** string REQUIRED
  A destination action

- **payload** object REQUIRED
  The body of the message

#### Example
```json
{
  "sender": {
    "host": "host2.example.com",
    "protocol": "example",
    "service": "repository"
  },
  "id": "abcdefghij",
  "reply-to": "0123456789",
  "host": "host1.example.com",
  "protocol": "example",
  "service": "form",
  "payload": {
    "status": "ok"
  }
}
```

## Connection protocol
*Connection protocol* specifies how to establish a connection between two different hosts with authentication.
The namespace of connection protocols' identifiers is case-insensitive.

### Specification
A specification of connection protocol contains following descriptions:

- REQUIRED its name
- REQUIRED its identifier
- REQUIRED its version
- REQUIRED how to establish a connection and how to transmit
- OPTIONAL parameters to configure.

A identifier MUST be a lowercase [a-z] string joined by '-',
and a version MUST be a semver.

## Service protocols
*Service protocol* specifies its own services and messages.
The namespace of service protocols' identifiers is case-insensitive.


### Specification
A specification of service protocol contains the following descriptions:

- REQUIRED its name
- REQUIRED its identifier
- REQUIRED its version
- REQUIRED list of services
- REQUIRED list of actions
- REQUIRED timeout and retransmission strategy
- OPTIONAL parameters.

A identifier, services, and actions MUST be a lowercase [a-z] string joined by '-',
and a version MUST be a semver.

### Subprotocols
A service protocol may have subprotocols.
Subprotocols are like extension of a service protocol.
If a service protocols has subprotocols,
it SHOULD have parameters with `-subprotocols` postfix
in the top level of the service protocol parameters.

#### Example
- **content-type-subprotocols** array REQUIRED
  An array of objects which have the following properties
  Same connection protocols with different versions are allowed.

  - **identifier** string REQUIRED
    The identifier of the subprotocol

  - **version** semver REQUIRED
    The version of the subprotocol

  - **parameters** object OPTIONAL
    The parameters for the subprotocol

### Compatibility
Each service protocol SHOULD make efforts to keep the compatibility between different versions
because messages don't have the proprety to specify the version of service protocol.
