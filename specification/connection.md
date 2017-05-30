# Connection

Each host must establish a *connection* first to communicate between two different hosts and transmit packets under the connection.
Yayaka Protocol doesn't specify the details of how to do that and each connection subprotocols do.

## Creating a connection

To create a connection, any common connection protocol which are specified in the host informations can be used.
Hosts SHOULD ignore connections which aren't specified in their host informations.
