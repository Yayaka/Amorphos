# Packet

A *packet* is a JSON data transferred between two different hosts under a connection.
It includes any number of messages.


## JSON format

### Properties

A packet is an object have following properties.

- MUST **messages** array  
  An array of messages

- SHOULD NOT all other properties

### Example

```
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
