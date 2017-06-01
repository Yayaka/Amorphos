# Message protocols

*Message protocol* specifies additional types of events and additional services.


## Specification

A specification of message protocol MUST contain its name, its version, a list of services, and list of actions and MAY contain parameters to configure.
A name, services, and actions SHOULD match the regular expression "[a-z0-9-]+" and a version MUST be a semver.


## Subprotocols

If a message protocols has subprotocols, they SHOULD be specified in its parameters in a similar format of host informations.


## Compatibility

Messages don't have the proprety to specify the version of message protocol.
Each message protocol SHOULD make efforts to keep the compatibility between different versions.
