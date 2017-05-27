# Yayaka Protocol Specification

## Glossary

This is a glossary of the basic terms in Yayaka Protocol.

### Yayaka services

*Yayaka services* are sets of related functions which can perform as one service.

### Host

A *host* is a server which implements one or more yayaka services and has a unique hostname.

### User

A *user* is registered at a host's *Identity service*.


## Communication

Layers to communicate between two host or two yayaka services.

### [Host informations](host-informations.md)

*Host informations* show the specification of a host.

### [Connection](connection.md)

Each hosts must establish a *connection* first to communicate.

### [Packet](packet.md)

A *packet* is a JSON data transferred between two different hosts under a connection.

### [Message](message.md)

A *message* is a JSON data transfered between two yayaka services.


## Yayaka services

There are following 5 services.

### [Identity service](identity-service.md)

*Identity service* works like a ID provider.

### [Repository service](repository-service.md)

*Repository service* works like a blogging service.

### [Social Graph service](social-graph-service.md)

*Social Graph service* stores users' relations and deliver events to followers.

### [Multimedia service](multimedia-service.md)

*Multimedia service* stores multimedia contents like images, movies, and so on.

### [Presentation service](presentation-service.md)

*Presentation service* works like an API client.


## Layered subprotocols

There are following types of subprotocol.
They have theirs own namespaces.

### [Connection subprotocol](connection-subprotocol.md)

*Connection subprotocol* specifies how to authenticate a host from other host.

### [Message subprotocol](message-subprotocol.md)

*Message subprotocol* specifies additional types of events.

### [Text subprotocol](text-subprotocol.md)

*Text subprotocol* specifies additional types of contents.
