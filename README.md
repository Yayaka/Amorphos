# Yayaka Protocol

Yayaka Protocol is a yet another protocol for highly distributed social blogging.
It enables each instances not to have to implement all functions of distributed social blogging.

Yayaka Protocol is inspired by [HVDSGM (ja)](https://hakabahitoyo.wordpress.com/2017/05/22/hvdsgm/).

Currently, Yayaka Protocol is not have a version to release because it's unfinished.

## Features

- Each instances don't have to implement all functions of distributed social blogging.
- It doesn't force to use a specific protocol to send messages.


## Implementations

Implementations of Yayaka Protocol haven't existed yet but [Yayaka.net](https://yayaka.net) plans to implement it.


## Contributing

See [CONTRIBUTING](CONTRIBUTING.md).

## Glossary

This is a glossary of the basic terms in Yayaka Protocol.

### Yayaka parts

*Yayaka parts* are sets of related functions which can perform as one service.

### Host

A *host* is a server which implements one or more yayaka parts and has a unique hostname.

### User

A *user* is registered at a host's *Identity part*.


## Yayaka parts

Yayaka Protocol has several yayaka parts.
The parts are not special but they are usually united as one service.
Yayaka Protocol allows them to be distributed into multiple hosts.
They communicates each other with messages.

There are following 5 parts.

- [Identity part](#identity-part)
- [Repository part](#repository-part)
- [Social Graph part](#social-graph-part)
- [Multimedia part](#multimedia-part)
- [Presentation part](#presentation-part)

### Identity part

*Identity part* works like a ID provider.
It stores users' profile and authenticated hosts.

Each user register themselves at one of hosts which has identity part.

### Repository part

*Repository part* works like a blogging service.
It only stores text data.

Each user can authenticate any number of hosts as a repository part.

### Social Graph part

*Social Graph part* stores users' relations and deliver events to followers.

Each user can authenticate only one host as a social graph part.

### Multimedia part

*Multimedia part* stores multimedia contents like images, movies, and so on.

### Presentation part

*Presentation part* works like a client.
It collects and subscribes timeline posts and notifications.

Each user can authenticate any number of presentation host users.


## License

 <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
