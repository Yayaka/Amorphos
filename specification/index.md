# Yayaka Protocol Specification

## Glossary

This is a glossary of the basic terms in Yayaka Protocol.

### Services

*Services* are sets of related functions which can perform as one service.
They can be united on a same host and also be distributed into multiple hosts.

### Host

A *host* is a server which implements one or more services and has a unique hostname.

### User

A *user* is registered at a host's *Identity service*.


## Communication

Layers to communicate between two host or two services.

To tell the truth, this section is an only essential part of Yayaka Protocol specification.
Other sections are treated as a reserved subprotocols

### [Host metadata](host-metadata.md)

### [Connection](connection.md)

### [Packet](packet.md)

### [Message](message.md)


## Layered subprotocols

There are following types of subprotocol and they have theirs own namespaces which is case-insensitive.
Root subprotocols can have owned services and all subprotocols can allow their categorised subprotocols.

### [Connection subprotocol](connection-subprotocol.md)

### [Message subprotocol](message-subprotocol.md)


## Reserved subprotocols

### [Yayaka subprotocol](yayaka-subprotocol.md)

*Yayaka subprotocol* is a message subprotocol
which provides several services and messages for highly distributed social blogging.
