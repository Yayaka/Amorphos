# Yayaka subprotocol

*Yayaka subprotocol* is for highly distributed social blogging.

## Name

yayaka

## Version

0.1.0

## Services

There are following 5 services.

### Identity service

An *identity service* works like a ID provider.
It stores users' profile, token, and authenticated hosts.

Each user register themselves at one of hosts which has identity service.

### Repository service

A *repository service* works like a blogging service.
It only stores contents.

Each user can authenticate any number of hosts as a repository service.

### Social graph service

A *social Graph service* stores users' relations and deliver events to followers.

Each user can authenticate only one host as a social graph service.

### Presentation service

A *presentation service* is an application having a user interface.
It collects and subscribes timeline posts and notifications.

Each user can authenticate any number of presentation host users.

### Actions

Each services SHOULD ignore actions which don't fillful the following conditions.

#### create-user

An action to create a user.

- Destination MUST be an identity service.
- Sender MUST be from the same host.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **attribute** string
    - MUST **value** string

#### update-user-attributes

An action to update the user profile.

- Destination MUST be an identity service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **attribute** string
    - MUST **value** string

#### delete-user-attributes

An action to update the user profile.

- Destination MUST be an identity service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **attribute** string

#### fetch-user

An action to fetch user's profile and trust list.

- Destination MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string

#### get-token

An action to fetch a token for trust a service by a user.

- Destination MUST be an identity service.
- Sender MUST be from the same host.
- Payload have following properties.
  - MUST **user-id** string

#### trust-you

An action to let a user to trust a service from an identity service.

- Sender MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **service** string
  - MUST **parameters** object

#### trust-me

An action to let a user to trust a service from a service.

- Destination MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **token** string
  - MUST **host** string
  - MUST **protocol** string
  - MUST **service** string
  - MUST **parameters** object

#### revoke-trust

An action to revoke a trust.

- Destination MUST be an identity service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **protocol** string
  - MUST **service** string

#### check-trust

An action to check wheather a service is trusted or not.

- Destination MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **protocol** string
  - MUST **service** string

#### create-event

An action to add an event.

- Destination MUST be a repository service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **parameters** object

#### broadcast-event

An action to broadcast an event.

- Destination MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **event-id** string
  - MUST **host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **parameters** object

#### fetch-event

An action to fetch an event.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **event-id** string

#### fetch-events

An action to fetch events.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **host** string
      - MUST **user-id** string
    - MUST **protocols** array
    - MUST **types** array

#### fetch-content

An action to fetch a content.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **content-id** object

#### follow-user

An action to follow a user.

- Destination MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties
  - MUST **user-id** string
  - MUST **host** string
  - MUST **target-user-id** string

#### unfollow-user

An action to unfollow a user.

- Destination MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties
  - MUST **user-id** string
  - MUST **host** string
  - MUST **target-user-id** string

#### follow-remote-user

An action to follow a remote user.

- Destination MUST be a social graph service.
- Sender MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties
  - MUST **user-id** string
  - MUST **host** string
  - MUST **target-user-id** string

#### unfollow-remote-user

An action to unfollow a remote user.

- Destination MUST be a social graph service.
- Sender MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties
  - MUST **user-id** string
  - MUST **host** string
  - MUST **target-user-id** string

#### fetch-user-relations

Ac action to fetch the relations of a user.

- Destination MUST be a social graph service.
- Payload have following properties
  - MUST **user-id** string

#### collect-events

An action to collect events.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **host** string
      - MUST **user-id** string
    - MUST **protocols** array
    - MUST **types** array

#### subscribe-evnets

An action to request and subscribe events.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **available-seconds** integer
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **host** string
      - MUST **user-id** string
    - MUST **protocols** array
    - MUST **types** array

#### unsubscribe-events

An action to unsubscribe events.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **subscription-id** string

#### extend-events-subscription

An action to extend a subscription.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **subscription-id** string
  - MUST **available-seconds** integer

## Subprotocols

### Profile protocols

A *profile protocol* specifies additional attributes of profiles.

### Event protocols

A *event protocol* specifies additional types of events.

### Presentation protocols

A *presentation protocol* specifies additional types of contents to show.
