# Yayaka Protocol Specification

## Introduction

Yayaka Protocol is a yet another protocol for highly distributed web applications especially social blogging.
It enables each instances not to have to implement all functions of distributed web application.

Yayaka Protocol focuses on minimum specification and higher extensibility by subprotocols.


## Encoding

Yayaka Protocol uses JSON format with UTF-8 encoding.


## Glossary

This is a glossary of the basic terms in Yayaka Protocol.

<dl>
<dt>Host
<dd>
A <i>host</i> is a server which implements any number of services and has a unique hostname.
</dd>

<dt>Protocol
<dd>
We call message subprotocols just "protocols" for convenience.
A <i>protocol</i> specifies own services and types of messages.
</dd>

<dt>Service
<dd>
A <i>service</i> is a set of related functions which can perform as one service.
They can be united on a same host and also be distributed into multiple hosts.
</dd>
</dl>


## Communication

There are several layers to communicate between two hosts or two services.

To tell the truth, this section is an only essential part of Yayaka Protocol specification.
Other sections are treated as a reserved subprotocols

### [Host](host.md)

### [Connection](connection.md)

### [Packet](packet.md)

### [Message](message.md)


## Layered subprotocols

There are following types of subprotocol and they have theirs own namespaces which is case-insensitive.

### [Connection protocol](connection-protocol.md)

### [Message protocol](message-protocol.md)


## Reserved subprotocols

### [Yayaka subprotocol](yayaka-subprotocol.md)

*Yayaka subprotocol* is a message protocol
which provides several services and messages for highly distributed social blogging.
