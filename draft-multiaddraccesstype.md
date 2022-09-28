---
title: Definition of the Multiaddress MIME External-Body Access-Type
abbrev: MultiaddrAccessType
docname: draft-multiaddraccesstype-latest
date: 2022-09-27

ipr: trust200902
area: Applications
workgroup: Invdividual Submission
category: std
keyword:
 - Internet-Draft
 - multiaddress
 - multiaddr
 - accesstype

author:
 - fullname: Gavin John
   email: gavinnjohn@gmail.com

normative:
  RFC1521:
  MULTIADDR:
    target: https://multiformats.io/multiaddr/
    title: Multiaddress Specification
    author: false
    date: false
    seriesinfo:
      Web: https://multiformats.io/multiaddr/
      Github: https://github.com/multiformats/multiaddr
informative:
  RFC4289:
entity:
  SELF: "[I-D.multiaddraccesstype]"

v: 3
venue:
  github: Pandapip1/multiaddr-access-type
  latest: https://Pandapip1.github.io/multiaddr-access-type/draft-multiaddraccesstype.html

--- abstract

This document defines a new access-type for message/external-body MIME parts for human-readable multiaddresses (multiaddrs). Multiaddrs provide future-proof, composable, and efficient content addresses. An initial list of supported protocols can be found in the multiaddress specification.

--- middle

# Introduction

TODO Introduction

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Security Considerations

TODO Security

# IANA Considerations

This draft adds the following access type to the Access Types registry of {{?RFC4289}}:

| Access Type Name |	Reference |
|-----------------:+-----------|
| multiaddr        | {{&SELF}} |

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
