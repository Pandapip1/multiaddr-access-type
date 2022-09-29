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
   
 - fullname: Ned Freed
   org: Innosoft International, Inc.
   email: ned@innosoft.com
   phone: +1 818 919 3600
   street: 1050 East Garvey Avenue South
   city: West Covina, CA
   code: 91790
   country: USA
   
 - fullname: Keith Moore
   org: University of Tennessee
   email: moore@cs.utk.edu
   street: 107 Ayres Hall
   city: Knoxville, TN
   code: 37996-1301
   country: USA

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
  RFC2017:
entity:
  SELF: "[I-D.multiaddraccesstype]"

v: 3
venue:
  github: Pandapip1/multiaddr-access-type
  latest: https://Pandapip1.github.io/multiaddr-access-type/draft-multiaddraccesstype.html

--- abstract

This document defines a new access-type for `message/external-body` MIME parts for human-readable multiaddresses (multiaddrs). Multiaddrs provide future-proof, composable, and efficient content addresses. An initial list of supported protocols can be found in the multiaddress specification.

--- middle

# Introduction

The Multipurpose Internet Message Extensions (MIME) define a facility whereby an object can contain a reference or pointer to some form of data rather than the actual data itself. This facility is embodied in the `message/external-body` media type defined in {{!RFC1521}}. Use of this facility is growing as a means of conserving bandwidth when large objects are sent to large mailing lists.

Each `message/external-body` reference must specify a mechanism whereby the actual data can be retrieved. These mechanisms are called access types, and {{!RFC1521}} defines an initial set of access types.

Multiaddresses, or multiaddrs, also provide a means by which remote data can be retrieved automatically. Multiaddrs support addresses for any network protocol, are self-describing, conform to a simple syntax, have human-readable and efficient machine-readable representations, and encapsulate well. For the purposes of this document, human-readable multiaddrs are used since they are more formally defined.

Multiaddrs are exclusively used for content addressing, so considerations about only using mechanisms that retrieve data do not apply.

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

The content of this document was heavily derived from {{?RFC2017}}. The authors of that RFC have been added as authors of this document, but have not reviewed nor endorsed it.
