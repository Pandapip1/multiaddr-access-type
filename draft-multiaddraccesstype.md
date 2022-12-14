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
  RFC822:
  RFC1521:
  RFC1738:
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

The Multipurpose Internet Message Extensions (MIME) define a facility whereby an object can contain a reference or pointer to some form of data rather than the actual data itself. This facility is embodied in the `message/external-body` media type defined in {{!RFC1521}}. Use of this facility is growing as a means of conserving bandwidth in various situations.

Each `message/external-body` reference must specify a mechanism whereby the actual data can be retrieved. These mechanisms are called access types, and {{!RFC1521}} defines an initial set of access types.

Multiaddresses, or multiaddrs, also provide a means by which remote data can be retrieved automatically. Multiaddrs support addresses for any network protocol, are self-describing, conform to a simple syntax, have human-readable and efficient machine-readable representations, and encapsulate well. For the purposes of this document, human-readable multiaddrs are used since they are more formally defined.

Multiaddrs are exclusively used for content addressing, so considerations about only using mechanisms that retrieve data do not apply.

# Definition of the Multiaddr Access-Type

{::boilerplate bcp14-tagged}

The multiaddr access type is defined as follows:

1. The name of the access type is "`multiaddr`".
2. A new `message/external-body` `content-type` parameter is used to actually store the multiaddress string. The name of the parameter is also "`multiaddr`", and this parameter is mandatory for this access type. The syntax and use of this parameter is specified in the next section.
3. The phantom body area of the `message/external-body` is not used and should be left blank.

For example, the following message illustrates how the multiaddr `access-type` is used:

```text
Content-type: message/external-body; access-type=multiaddr; multiaddr="/http/example.com/index.html"
```

## Syntax and Use of the `multiaddr` parameter

Using the ANBF notations and definitions of {{!RFC822}} and {{!RFC1521}}, the syntax of the `multiaddr` parameter is as follows:

```text
multiaddr-parameter := <"> multiaddr-word *(*LWSP-char multiaddr-word) <">

multiaddr-word := token
                 ; Must not exceed 40 characters in length
```

The syntax of an actual multiaddr string is given in {{MULTIADDR}}. Multiaddr strings can be of any length and can contain arbitrary character content. This presents problems when multiaddrs are embedded in MIME body part headers that are wrapped according to {{!RFC822}} rules. For this reason they are transformed into a `multiaddr-parameter` for inclusion in a `message/external-body` content type specification as follows:

1. A check is made to make sure that all occurrences of SPACE, CTLs, double quotes, backslashes, and 8-bit characters in the multiaddr string are encoded using the URL encoding scheme specified in {{!RFC1738}}. Any unencoded occurrences of these characters must be encoded. Note that the result of this operation results may result in a multiaddr that is different than the original, and will need to be decoded.
2. The resulting multiaddr string is broken up into substrings of 40 characters or less.
3. Each substring is placed in a `multiaddr-parameter` string as a `multiaddr-word`, separated by one or more spaces. The enclosing quotes are always included for consistency.

Extraction of the multiaddr string from the `multiaddr-parameter` follows a similar process:

1. The enclosing quotes are removed.
2. Any linear whitespace is removed.
3. The remaining material is decoded using the URL decoding scheme specified in {{!RFC1738}}. The result of this operation is the original multiaddr.

The following example shows how a long muliaddr is handled:

```text
Content-type: message/external-body; access-type=multiaddr;
              multiaddr="/dns4/example.com/tcp/443/tls/sni/exampl
                   e.com/http/example.com/index.html"

Content-type: text/html
Content-Transfer-Encoding: binary

THIS IS NOT REALLY THE BODY!
```

Some multiaddrs may provide access to multiple versions of the same object in different formats. The HTTP protocol has this capability, for example. However, applications may not expect to receive something whose type doesn't agree with that expressed in the `message/external-body`, and may in fact have already made irrevocable choices based on this information.

Due to these considerations, the following restriction is imposed: When multiaddrs are used in the context of an access type, only those versions of an object whose content type agrees with that specified by the inner `message/external-body` header can be retrieved and used.

# Rationale

The `message/external-body` MIME type is useful as it is a well-defined mechanism for referencing external data. Referencing external data itself is useful:

- Unnecessary bandwidth usage is avoided by not requesting and sending the same data.
- When there are multiple data locations, clients can select the fastest one.
- Senders can serve data that they can't access themselves.
  - This may be particularly useful for sandboxed or blockchain-based servers.

# Security Considerations

The security considerations of using multiaddrs in the context of a MIME access type are no different from the concerns that arise from their use in other contexts.

# IANA Considerations

This draft adds the following access type to the Access Types registry of {{?RFC4289}}:

| Access Type Name | Reference |
|-----------------:+-----------|
| multiaddr        | {{&SELF}} |

--- back

# Acknowledgments

The content of this document was heavily derived from {{?RFC2017}}. The authors of that RFC have been added as authors of this document, but have not reviewed nor endorsed it.
