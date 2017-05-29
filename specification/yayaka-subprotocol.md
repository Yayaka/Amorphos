# Yayaka subprotocol

*Yayaka subprotocol* specifies micro

## Services

There are following 5 services.

### Identity service

An *identity service* works like a ID provider.
It stores users' profile and authenticated hosts.

Each user register themselves at one of hosts which has identity service.

### Repository service

A *repository service* works like a blogging service.
It only stores text data.

Each user can authenticate any number of hosts as a repository service.

### Social Graph service

A *social Graph service* stores users' relations and deliver events to followers.

Each user can authenticate only one host as a social graph service.

### Multimedia service

A *multimedia service* stores multimedia contents like images, movies, and so on.

### Presentation service

A *presentation service* is an application having a user interface.
It collects and subscribes timeline posts and notifications.

Each user can authenticate any number of presentation host users.

## Subprotocols

### Presentation protocol

A *presentation protocol* specifies additional types of contents to show.
