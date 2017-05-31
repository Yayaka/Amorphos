# Yayaka Protocol

Yayaka Protocol is a yet another protocol for highly distributed social blogging.
It enables each instances not to have to implement all functions of distributed social blogging.
It's also for **any type** of highly distributed web application.

Yayaka Protocol is inspired by [HVDSGM (ja)](https://hakabahitoyo.wordpress.com/2017/05/22/hvdsgm/).

Currently, Yayaka Protocol is not have a version to release because it's unfinished.


## Features

- Minimum specification
- Extensible by layered and recursive subprotocols
- JSON


## Concepts

### Yayaka services

Yayaka Protocol has several yayaka services.
The yayaka services are not special but they are united as one web service generally.
Yayaka Protocol allows them to be distributed into multiple hosts.

### Layered subprotocols

Layered subprotocols allow us to create additional ways to communicate between two different hosts,
services which are different from yayaka services, types of events, and types of contents.


## Specification

- [Yayaka Protocol Specification](specification/index.md).


## Implementations

Implementations of Yayaka Protocol haven't existed yet but [Yayaka.net](https://yayaka.net) plans to implement it.


## Contributing

See [CONTRIBUTING](CONTRIBUTING.md).

## License

<p xmlns:dct="http://purl.org/dc/terms/" xmlns:vcard="http://www.w3.org/2001/vcard-rdf/3.0#">
  <a rel="license"
     href="http://creativecommons.org/publicdomain/zero/1.0/">
    <img src="http://i.creativecommons.org/p/zero/1.0/88x31.png" style="border-style: none;" alt="CC0" />
  </a>
  <br />
  To the extent possible under law,
  <a rel="dct:publisher"
     href="https://github.com/Yayaka">
    <span property="dct:title">Yayaka</span></a>
  has waived all copyright and related or neighboring rights to
  <span property="dct:title">Yayaka Protocol</span>.
This work is published from:
<span property="vcard:Country" datatype="dct:ISO3166"
      content="JP" about="https://github.com/Yayaka">
  日本</span>.
</p>
