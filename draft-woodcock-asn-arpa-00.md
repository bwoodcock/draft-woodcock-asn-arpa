---
title: "Delegation of the 'asn.arpa' Domain"
abbrev: "asn.arpa"
docname: draft-woodcock-asn-arpa-00
category: std
updates: 5855
consensus: true
submissiontype: IETF
ipr: trust200902
area: "Internet"
workgroup: "Domain Name System Operations"
keyword:

 - DNS
 - DNSSEC
 - autonomous system number
 - digital emblem
 - routing security
 - RIR
stand_alone: yes
smart_quotes: no
pi: [toc, sortrefs, symrefs, docmapping]

venue:
  group: "Domain Name System Operations"
  type: "Working Group"
  mail: "dnsop@ietf.org"

author:
 -
    ins: B. Woodcock
    name: Bill Woodcock
    organization: Packet Clearing House
    email: woody@pch.net
 -
    ins: M. Kosters
    name: Mark Kosters
    organization: ARIN
    email: markk@arin.net
 -
    ins: C. Martinez-Cagnazzo
    name: Carlos Martinez-Cagnazzo
    organization: LACNIC
    email: carlos@lacnic.net
 -
    ins: M. A. Tamon
    name: Mukom Akong Tamon
    organization: AFRINIC
    email: tamon@afrinic.net
 -
    ins: G. Huston
    name: Geoff Huston
    organization: APNIC
    email: gih@apnic.net

normative:
  RFC1034:
  RFC1035:
  RFC1930:
  RFC2181:
  RFC2308:
  RFC3172:
  RFC4034:
  RFC4592:
  RFC5155:
  RFC5396:
  RFC5398:
  RFC5855:
  RFC5936:
  RFC6793:
  RFC6996:
  RFC7300:
  RFC7344:
  RFC7607:
  RFC8078:
  RFC8945:
  RFC9103:
  RFC9364:
  RFC9904:

informative:
  RFC2317:
  RFC2535:
  RFC2622:
  RFC2860:
  RFC3152:
  RFC3219:
  RFC4012:
  RFC6480:
  RFC7020:
  RFC7050:
  RFC7249:
  RFC7454:
  RFC7535:
  RFC8198:
  RFC8375:
  RFC8767:
  RFC9120:
  RFC9156:
  RFC9224:
  RFC9499:
  RFC9520:
  RFC9812:
  I-D.ietf-diem-requirements:
  I-D.ietf-dnssec-as-map:
  DIEM-CHARTER:
    title: "Digital Emblems (diem) Working Group Charter"
    author:
      - org: Internet Engineering Task Force
    target: https://datatracker.ietf.org/wg/diem/about/
  IANA-ASN:
    title: "Autonomous System (AS) Numbers"
    author:
      - org: Internet Assigned Numbers Authority
    target: https://www.iana.org/assignments/as-numbers/
  IANA-ASN-SPECIAL:
    title: "Special-Purpose Autonomous System (AS) Numbers"
    author:
      - org: Internet Assigned Numbers Authority
    target: https://www.iana.org/assignments/iana-as-numbers-special-registry/
  IANA-ITAD:
    title: "IP Telephony Administrative Domain (ITAD) Numbers, in the Telephony Routing over IP (TRIP) Parameters registry"
    author:
      - org: Internet Assigned Numbers Authority
    target: https://www.iana.org/assignments/trip-parameters/
  ASN-ALLOC-POLICY:
    title: "Internet Assigned Numbers Authority (IANA) Policy for Allocation of ASN Blocks to Regional Internet Registries"
    author:
      - org: Internet Corporation for Assigned Names and Numbers
    date: 2010-09
    target: https://www.icann.org/resources/pages/global-policy-asn-blocks-2010-09-21-en
  ICP-2:
    title: "ICP-2: Criteria for Establishment of New Regional Internet Registries"
    author:
      - org: Internet Corporation for Assigned Names and Numbers
    date: 2001-06-04
    target: https://www.icann.org/resources/pages/new-rirs-criteria-2012-02-25-en
  ICP-2-REVIEW:
    title: "ICP-2 Review"
    author:
      - org: ICANN Address Supporting Organization Address Council
    target: https://aso.icann.org/icp-2-review/
  RIR-TRANSFERS:
    title: "Inter-Registry Transfer Statistics (each Regional Internet Registry publishes an equivalent file)"
    author:
      - org: The Regional Internet Registries
    target: https://ftp.ripe.net/pub/stats/ripencc/transfers/transfers_latest.json
  RIR-STATS:
    title: "NRO Extended Allocation and Assignment Report"
    author:
      - org: The Number Resource Organization
    target: https://ftp.ripe.net/pub/stats/ripencc/nro-stats/latest/nro-delegated-stats
  NRO-STATS-FORMAT:
    title: "NRO Extended Allocation and Assignment Report Format"
    author:
      - org: The Number Resource Organization
    target: https://www.nro.net/wp-content/uploads/nro-extended-stats-readme5.txt
  COM-ZONE:
    title: "The .com Zone File, distributed through the ICANN Centralized Zone Data Service"
    author:
      - org: VeriSign Global Registry Services
    target: https://czds.icann.org/
  STATDNS:
    title: "TLD Zone File Statistics, August 2026: monthly resource-record counts derived from the generic top-level domain zone files"
    author:
      - ins: F. Cambus
        name: Frederic Cambus
    date: 2026-08
    target: https://www.statdns.com/data/2026-08-tld-zone-file-statistics.csv
  INOC-DBA:
    title: "INOC-DBA: the Inter-Network Operations Center Dial-By-ASN hotline"
    author:
      - org: NIC.br
    target: https://inoc.nic.br/

--- abstract

This document requests the delegation of the "asn.arpa" domain and describes
the naming structure and administrative arrangements that apply to it. The
domain provides a stable, globally unique domain name associated with each Autonomous System Number (ASN), so that peering policies, digital emblems and other authenticated statements can be attached to autonomous systems. The zone is administered by IANA, which delegates a subdomain to each Regional Internet Registry and publishes a CNAME record for each allocated Autonomous System Number pointing into the subdomain of the RIR that administers it. Delegation of the corresponding nameserver domain 'asn-servers.arpa' is also requested.

--- middle

# Introduction

The Internet's globally unique number resources fall into three families: IPv4
addresses, IPv6 addresses, and Autonomous System Numbers (ASNs) {{RFC1930}}.
All three are distributed through the same hierarchy, the Internet Numbers
Registry System {{RFC7020}}, whose constituent IANA registries are identified
by {{RFC7249}} (updated by {{RFC9812}}): IANA allocates aggregate blocks to the Regional Internet Registries (RIRs), and each RIR assigns individual resources to
registrants in their region under community-developed policy.

Two of the three families already have corresponding namespaces in the DNS:
"in-addr.arpa" {{RFC1035}} for IPv4 and "ip6.arpa" {{RFC3152}} for IPv6.
To date, Autonomous System Numbers have none, and therefore lack a canonical place for the publication of authenticated policies or a name by which Uniform Resource Identifiers can reference them.

That absence blocks work elsewhere in the IETF. The Digital Emblems (DIEM) working group requires that a digital emblem identify assets by fully qualified domain name
{{I-D.ietf-diem-requirements}}. Autonomous systems are among the assets that
need to be marked, and at present they cannot be because, unlike IPv4 and IPv6 addresses, no domain identifies them. {{rationale}} develops this.

This document requests the delegation of "asn.arpa", specifies the structure of
the zone, and specifies the DNSSEC requirements that apply to it and to
delegations made from it. It does not define any resource record content;
applications of the namespace are expected to be specified separately, as
described in {{applications}}.

The document makes two further requests, both concerning the naming of
nameservers. It requests the delegation of "asn-servers.arpa", the zone that
names the nameservers of "asn.arpa", on the model established for the reverse
zones of the other two number resource families by {{RFC5855}}. And, because
that model was established in a Best Current Practice document rather than in
the Standards Track document that Section 3 of {{RFC3172}} contemplates, it
restates the existing delegations of "in-addr-servers.arpa" and
"ip6-servers.arpa", unchanged and with no operational effect, so that the
nameserver zones of all three number resource families are defined in a Standards Track document.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

DNS terminology is as defined in {{RFC9499}}. Autonomous System Numbers are
32-bit unsigned integers {{RFC6793}}, written throughout this document in the
"asplain" notation of {{RFC5396}}.

"RIR" means an organization recognized as a Regional Internet Registry through
the process described in {{ICP-2}}; see {{newrirs}}. "Registrant" means the
party to which a Regional Internet Registry has assigned an Autonomous System
Number, or which has received an Autonomous System Number via transfer from another Registrant. Of the two RIRs party to an inter-RIR transfer, the one from which the Autonomous System Number moves is the "source RIR" and the one to which it moves is the "recipient RIR".

This document uses "allocation" and "assignment" in the sense established by
the Internet Numbers Registry System {{RFC7020}} and does not use them
interchangeably. IANA *allocates*
blocks of Autonomous System Numbers to Regional Internet Registries. A Regional
Internet Registry *assigns* an individual Autonomous System Number to a
registrant. An ASN that has been allocated to an RIR but not yet assigned
to a registrant is *unassigned*; an ASN that has not been allocated to any
RIR remains *unallocated*, in the IANA pool. IANA has direct knowledge only of the allocations it performs; it learns of both RIR assignments and inter-RIR transfers second-hand.

# Rationale {#rationale}

## Digital Emblems for Autonomous Systems

The first and most immediate motivation for this document is the need to bind digital emblems
to autonomous systems. The Digital Emblems (DIEM) working group is chartered to define a means
by which such emblems can be discovered and validated for network-connected
assets {{DIEM-CHARTER}} {{I-D.ietf-diem-requirements}}, with discovery in the
initial scope performed through the DNS. The architecture requires that an
emblem be bound to the asset it marks by a fully qualified domain name.

Some of the assets that most need marking are autonomous systems. The network
of a hospital, of a civil defense organization, of a humanitarian agency, or of
a national or intergovernmental body enjoying protection under international law is, at the routing
layer, an autonomous system: a set of prefixes originated under a common
administration and identified by an Autonomous System Number. 

An emblem cannot be attached to an autonomous system today because an autonomous system has no fully qualified domain name to which it could be attached, and because there is no authority from whom such a name could be obtained that is congruent with the authority that assigned the ASN. This document supplies both. The name "64496.asn.arpa" would exist if AS 64496 were allocated; it would be delegated, through the RIR that assigned AS 64496, to the registrant of AS 64496; and the whole path is DNSSEC-signed, so a validator can establish that what it retrieved was published by that registrant.

The DIEM architecture cannot mark autonomous systems, as it was chartered to do, until autonomous systems can be named.

## Peering Policy and Other Uses

Once autonomous systems have names, other classes of authenticated statement
become possible. The most pressing of those is peering policy.

An operator's peering policy: whether open, selective, or restrictive;
where the operator is present; what it asks of a prospective peer; whom to
approach -- all of this is information about an autonomous system that other operators
consult routinely and act upon. It is published today in third-party databases
and in Internet Routing Registry (IRR) objects expressed in the Routing Policy
Specification Language {{RFC2622}}, extended for IPv6 and multicast address
families by RPSLng {{RFC4012}}, in forms that are not cryptographically bound
to the registrant of the autonomous system. No object
exists in RPKI for this purpose and none is contemplated, so nothing here
overlaps or competes with {{RFC6480}}.

Beyond peering policy there are operational and security contacts, references
to IRR objects, statements of BGP operations and security practices
{{RFC7454}}. {{I-D.ietf-dnssec-as-map}} proposed in 1997 that every Autonomous System Number be given a name in the DNS so that a KEY {{RFC2535}} record could be used to authenticate messages between autonomous systems
without pairwise pre-shared keys. In 2001 INOC-DBA {{INOC-DBA}} connected the responsible parties of some 3,800 ASNs using the SIP protocol, but required a central authority to guarantee identities, since no such name-and-key binding existed. The subsequent IANA registry of IP Telephony Administrative
Domain numbers {{RFC3219}} {{IANA-ITAD}} has served the same function with the same limitation. These and other uses are expected to be developed separately
and on their own merits, subject to {{applications}}.

## Relationship to RPKI

This namespace is not an authorization mechanism and is not a substitute for
RPKI {{RFC6480}}. The two structures have different trust properties.

## Relationship to RDAP

The service discovery mechanism of the Registration Data Access Protocol
(RDAP) uses a bootstrap file that IANA publishes under {{RFC9224}},
which maps ranges of Autonomous System Numbers to the base URLs of the RIRs'
RDAP services. The bootstrap file is generated from IANA's allocation
registry ({{RFC9224}}, Section 12), so it records the ranges as they were allocated to the RIRs and it does not reflect subsequent inter-RIR transfers. RDAP queries for transferred ASNs received by the source RIR are answered with an HTTP 303 redirect to the recipient RIR. That is the same device as the intermediate CNAME of {{deferred}}. The RDAP redirections are permanent, growing in number and length over time, whereas the CNAME delegation chains are periodically flattened.

The two mechanisms answer different questions for different consumers and do not compete. RDAP has no means of carrying a Digital Emblem, and RDAP has no equivalent of authenticated denial of existence. RDAP describes the registration while "asn.arpa" names the thing registered.

## Why Under "arpa"

The "arpa" domain is already intended for this class of use: an
infrastructural identifier space derived from a protocol family, administered
by IANA under IAB guidance {{RFC3172}} and within the scope of {{RFC2860}}, and
external to the commercial, contractual, and jurisdictional considerations
that complicate use of other parts of the domain name space. It is also the only
choice consistent with the treatment of the other two number resource families.
Previous delegations made under the same process include "ipv4only.arpa"
{{RFC7050}}, "empty.as112.arpa" {{RFC7535}}, and "home.arpa" {{RFC8375}}.

# Structure of the asn.arpa Zone {#structure}

## Overview

The "asn.arpa" zone contains:

* a delegation, with NS and DS RRsets, for each Regional Internet Registry
  ({{rirdelegations}});
* a CNAME record for each Autonomous System Number that has been allocated to a
  Regional Internet Registry, pointing into the subdomain of the RIR that
  administers it ({{cnames}}); and
* the records required to operate, secure, and sign the zone itself.

## Delegations to the Regional Internet Registries {#rirdelegations}

IANA delegates one subdomain of "asn.arpa" to each Regional Internet Registry.
The initial set is:

    afrinic.asn.arpa.       AFRINIC
    apnic.asn.arpa.         APNIC
    arin.asn.arpa.          ARIN
    lacnic.asn.arpa.        LACNIC
    ripe.asn.arpa.          RIPE NCC

Each is delegated to nameservers designated by the RIR concerned, and each
delegation is accompanied by a DS RRset as required by {{dnssec}}. The labels
are short forms of the RIRs' own names; an RIR that prefers a
different label for its subdomain may inform IANA; changing the RIR label is transparent to consumers. An RIR MUST NOT designate, for the zone delegated to it, a nameserver whose name is subordinate to "asn.arpa", so that zone requires no glue records and IANA holds no address records for infrastructure it does not operate.

These delegations are not associated with ranges of Autonomous System Numbers.
The association between an ASN and an RIR is expressed by the CNAME set
of {{cnames}}, and nothing in the delegation structure changes when ASNs are transferred between RIRs.

Each RIR administers the zone delegated to it in accordance with the policies
developed by its own community. Within that zone, the name corresponding to an
Autonomous System Number is the asplain decimal representation of that ASN as
a single label, "64496.arin.asn.arpa", which the RIR delegates to the
registrant of the ASN or serves directly.

## The Per-ASN CNAME Set {#cnames}

For each Autonomous System Number that has been allocated to a Regional
Internet Registry, IANA publishes a CNAME record in the "asn.arpa" zone. The
owner name of that record is the asplain decimal representation of that ASN,
as a single label; its target is the identically labeled name in the subdomain
of the administering RIR:

    64496.asn.arpa.     CNAME   64496.arin.asn.arpa.
    64497.asn.arpa.     CNAME   64497.ripe.asn.arpa.
    65536.asn.arpa.     CNAME   65536.apnic.asn.arpa.

In all cases, asplain notation {{RFC5396}} MUST be used. The "asdot" and
"asdot+" notations MUST NOT be used, and no prefix such as "AS" is used. There
is only one label in "asn.arpa" for each allocated Autonomous System Number.

Because a CNAME record cannot coexist with other non-DNSSEC RRTYPEs at the same label {{RFC1034}}{{RFC2181}}, no other data appear at these labels, and all data
concerning an Autonomous System Number is served from the RIR side of the
redirection.

Redirection of individual numerical identifiers by CNAME is long-established practice in the reverse namespace. {{RFC2317}}, Best Current Practice since 1998, delegates "in-addr.arpa" space on other than an octet boundary by publishing, in the enclosing zone, one CNAME per address of the delegated block, each pointing at the corresponding name in a zone operated by another party. What is described here differs only in that the redirection is per Autonomous System Number rather than per IP address, and that the subordinate zones are operated by the Regional Internet Registries; the mechanism, and the resolver behavior it depends upon, are the same.

The CNAME describes allocation and not assignment. IANA knows which RIR it allocated an ASN to; it has no knowledge of whether, or to whom, that RIR has assigned it. The CNAME is therefore published when the ASN is allocated to an RIR, and the corresponding name in the RIR's subdomain does not come into existence until the ASN has been assigned to a registrant. In the interval between allocation and assignment, and for as long after assignment as a registrant publishes nothing, the CNAME points at a name that does not exist. What can and cannot be inferred from that absence is set out in {{absence}}.

No CNAME is published for an ASN that has not been allocated to an RIR,
nor for one whose allocation has been returned to the IANA pool.

IANA MUST NOT publish any wildcard records {{RFC4592}} in "asn.arpa", and Regional
Internet Registries MUST NOT publish any in the zones delegated to them. A wildcard
in either zone would synthesize an answer at every name within its scope for
which nothing has been published, and would do so under the signature of an operator that does not hold the numbers concerned.

The asplain representation is concise and can be read and written by humans without additional tooling. Because it does not require transformation and errors are recognizable on sight, transcription errors are less likely to occur than if other encodings are used. These names are expected to appear in digital emblems and in the tools that validate them, in peering documents, and in correspondence, where these properties are inherently advantageous.

## The Stable Identifier of an Autonomous System {#canonical}

The name "&lt;asn&gt;.asn.arpa" is a stable reference to an Autonomous System
Number. The target of the CNAME is an artifact of which RIR currently
administers the ASN, and is subject to change.

Specifications and applications that need to refer to an autonomous system by
name SHOULD use the "&lt;asn&gt;.asn.arpa" form. The RIR-qualified form is not a stable identifier: it changes whenever the Autonomous System Number is transferred. The RIR-qualified form SHOULD NOT be recorded or embedded in a reference.

## Portability Between RIRs {#portability}

Autonomous System Numbers move between RIRs, both individually by
transfer and in aggregate when the RIR responsible for a region changes. Under
this system, these moves are reflected by a repointing of the "asn.arpa" CNAME by IANA.

The name of the autonomous system does not change, no delegation is
restructured, nothing that referred to the autonomous system by its stable identifier is invalidated, and any emblem or other statement attached to it survives the transfer. The recipient RIR publishes the data at the new target and the source RIR eventually withdraws it; see {{deferred}}.

The alternative would be to delegate ASN ranges to the RIRs, as "in-addr.arpa" and "ip6.arpa" do for IP addresses. Unlike address ranges, an ASN is assigned individually, and a transfer removes a single ASN from the interior of its enclosing range. Under any encoding that permits aggregation, that ASN cannot simply be moved: the range containing it must be broken into the aligned fragments remaining on either side, and a new delegation created for the ASN itself. Each transfer thus replaces a single delegation with approximately twenty-five, each carrying its own nameserver records, its own DS RRset, and its own key-rollover coordination between IANA and an RIR. There is no mechanism by which those fragments can be reassembled. Movement that has already occurred raises the count of delegations needed to cover the present distribution of Autonomous System Numbers among the RIRs from 891, the cover of IANA's own allocation blocks, to 16,670. 

## Deferred Repointing and Chain Depth {#deferred}

A transfer still takes effect the moment the two involved RIRs act; it does not immediately involve IANA. The source RIR publishes, within its own subdomain of "asn.arpa", a CNAME pointing to the corresponding name in the recipient RIR's subdomain of "asn.arpa":

    64496.arin.asn.arpa.    CNAME   64496.ripe.asn.arpa.

Resolution then follows a chain of two CNAMEs, from "64496.asn.arpa" to
"64496.arin.asn.arpa" and from there to "64496.ripe.asn.arpa". IANA repoints the
parent CNAME at its own convenience, presumably in the same zone edit as its next block allocation, after which the source RIR waits at least the TTL period (but within the same flattening cycle) and then withdraws the intermediate CNAME. No additional IANA-to-RIR notification mechanism is needed to effect the source-RIR withdrawal, since IANA already announces each allocation event to the RIRs and to the public, RIRs monitor these announcements already, and the repointing occurs in the same edit.

This ensures that IANA's edit rate is decoupled from transfer activity. IANA's
operations on "asn.arpa" would presumably consist of approximately five editing operations per year, paralleling the ASN allocation rate, which has been effectively flat for the past two decades {{ASN-ALLOC-POLICY}} {{IANA-ASN}} and which does not change under this system.

The flattening operation is invisible to resolvers: a cache still
holding the parent CNAME reaches the intermediate one and resolves correctly,
so IANA may batch flattening on its own schedule with no coordination window
and no risk of a stale answer being wrong.

The DNS sets no limit on the length of a CNAME chain, and implementations
therefore impose their own, most choosing limits between ten and sixteen hops, counted across the whole of a resolution and shared with DNAME.

This system uses either a single CNAME or a CNAME chain of two hops. A third would require the same Autonomous System Number to be transferred between RIRs twice within a single flattening interval: approximately ten weeks. Although 1,909 ASNs have been transferred once (1,722 pre-2018 ERX, and 187 post-2018 transfers), no ASN has yet been transferred more than once. Thus a second transfer (and third CNAME hop) of the same ASN within ten weeks is very unlikely, and a third transfer within ten weeks is not plausible. Nonetheless, up to nine transfers of the same ASN could be effected within a single flattening window without ill effect.

An RIR that receives an inbound transfer of an Autonomous System Number
that it had previously transferred away MUST withdraw its own outbound CNAME
for that ASN, rather than leaving it in place. Where the RIR has
records to publish at that label, the exclusivity rule of {{RFC1034}} compels
this in any case, since a CNAME cannot coexist with other non-DNSSEC resource records at the same label; but an RIR with nothing to publish is not so compelled, and so without this restriction, two RIRs each retaining an outbound CNAME for the same ASN could form a loop that no resolver could resolve.

An intermediate CNAME MUST NOT be published for any purpose other than a
completed transfer awaiting flattening, and MUST NOT point to a name outside
"asn.arpa". It is the only CNAME an RIR may publish at an Autonomous
System Number name; see {{models}}.

## Special-Purpose and Unallocated Autonomous System Numbers

No CNAME is published, and the zone returns authenticated denial of existence,
for Autonomous System Numbers reserved for special purposes. At the time of
writing these are:

* AS 0 {{RFC7607}};
* AS 23456, reserved for representation of 4-octet ASNs to legacy speakers
  {{RFC6793}};
* AS 64496 through AS 64511 and AS 65536 through AS 65551, reserved for
  documentation {{RFC5398}};
* AS 64512 through AS 65534 and AS 4200000000 through AS 4294967294, reserved
  for private use {{RFC6996}};
* AS 65535 and AS 4294967295 {{RFC7300}}.

The "Special-Purpose Autonomous System (AS) Numbers" registry
{{IANA-ASN-SPECIAL}}, established by Section 3 of {{RFC7249}}, is
authoritative for which ASNs those are, and IANA reflects changes to it in the
zone.

## New, Divided, and Derecognized RIRs {#newrirs}

Although change is infrequent, the set of delegations in {{rirdelegations}} is not fixed. If a new Regional Internet Registry is recognized, IANA adds a delegation for it, using a label derived from the RIR's name, and repoints the CNAMEs of the Autonomous System Numbers it administers. If an existing RIR is divided or derecognized, the same operations apply. Recognition and derecognition of Regional Internet Registries is a matter for the ICANN Address Supporting Organization process, not for this document or for the IETF; see {{ICP-2}} and the revision under way at the time of writing {{ICP-2-REVIEW}}.

No Autonomous System Number's stable identifier is affected by any of these
events, as a direct consequence of {{portability}}.

# Nameservers for the Number Resource Zones {#servers}

## Nameservers for "asn.arpa" {#asnservers}

The nameservers that serve the "asn.arpa" zone are named within a dedicated
subdomain of "arpa", following the arrangement made for "in-addr.arpa" and
"ip6.arpa" by {{RFC5855}}. The initial set is "a.asn-servers.arpa" through
"e.asn-servers.arpa", extended alphabetically if further servers are added. This allows the NS RRset of 'asn.arpa' to be expressed entirely in names that IANA administers for the purpose, so that the servers behind those names can be changed without a change to the 'arpa' zone.  This is a naming scheme, not a requirement to operate distinct infrastructure. 

## Nameservers for "in-addr.arpa" and "ip6.arpa" {#existingservers}

"in-addr-servers.arpa" and "ip6-servers.arpa" name the nameservers of
"in-addr.arpa" and "ip6.arpa" respectively. IANA delegated both in 2010, with
the approval of the IAB, as specified in Sections 2, 3, and 5 of {{RFC5855}},
and both have been in continuous operation since; each is signed, with a DS
RRset in the "arpa" zone. The naming schemes are "a.in-addr-servers.arpa"
through "f.in-addr-servers.arpa" and "a.ip6-servers.arpa" through
"f.ip6-servers.arpa", extended alphabetically if further servers are added.

{{RFC5855}} is a Best Current Practice document. Section 3 of {{RFC3172}}
specifies that the IAB shall recommend creation of a subdomain of "arpa" where
the delegation and the hierarchical name structure are described by an IETF
Standards Track document whose IANA Considerations section explicitly
recommends the use of "arpa". The IAB treated the two delegations as an
operational change rather than as the creation of a namespace for protocol
objects, and approved them on that basis (Section 4 of {{RFC5855}}).

This document restates those two delegations so that the nameserver zones of
all three number resource families are described by a Standards Track
document, as this document
does for "asn-servers.arpa". Nothing is altered by the restatement: the
delegations, their nameserver sets, the naming schemes of Sections 2 and 3 of
{{RFC5855}}, and the operation of the two zones remain exactly as they are today.
No new action is required of IANA with respect to them.

# DNSSEC Requirements {#dnssec}

The utility of this namespace depends upon the integrity of the data
published within it, and therefore upon DNSSEC {{RFC9364}}. Accordingly:

* The "asn.arpa" and "asn-servers.arpa" zones MUST be signed by IANA, and DS RRsets for them MUST be present in the "arpa" zone. There MUST NOT be
  any interval during which "asn.arpa" or "asn-servers.arpa" exist as insecure delegations.
* Every delegation published in the "asn.arpa" zone MUST be accompanied by a DS
  RRset. Insecure delegations MUST NOT be created in "asn.arpa", and a
  delegation whose DS RRset is withdrawn MUST be removed rather than left
  insecure.
* Each Regional Internet Registry MUST sign the zone delegated to it, and MUST
  maintain a current DS relationship with IANA across key rollovers. IANA
  SHOULD support maintenance of these DS RRsets by means of CDS and CDNSKEY
  records {{RFC7344}} {{RFC8078}}, and MUST operate a documented
  process by which an RIR can effect a DS change without an insecure
  interval.
* Each Regional Internet Registry MUST publish valid DS RRsets supplied to it by registrants, and SHOULD support maintenance of that DS RRset by means of CDS
  and CDNSKEY records {{RFC7344}} {{RFC8078}}.
* The registrant of an Autonomous System Number SHOULD sign the zone delegated
  to it and supply the DS RRset for it to the RIR.
* Signing MUST use algorithms consistent with current DNSSEC algorithm guidance
  {{RFC9904}}.

No separate trust anchor is created by this document. Validation proceeds from
the root zone trust anchor through "arpa" in the ordinary way, and implementations MUST NOT be configured with "asn.arpa" or any zone beneath it as an independent trust anchor.

# Applications of the Namespace {#applications}

This document creates the namespace and the structure. It defines no resource
record types and no record content, and publication of anything under a
delegated name is outside its scope.

Documents specifying content to be published under "asn.arpa" are subject to
the normal IETF process, and are expected to address at minimum: the record
types used, their placement, and the behavior of a consumer on encountering unexpected data.

# Operational Considerations

## Zone Contents and Provisioning

The "asn.arpa" zone holds one delegation per Regional Internet Registry (five at the time of writing), each comprising an NS RRset and a DS RRset; and one CNAME per allocated Autonomous System Number (approximately 140,000 at time of writing) {{IANA-ASN}}. No glue records are required, because the nameservers of the RIR subdomains are named outside "asn.arpa" ({{rirdelegations}}). The zone is mechanically generated, and of modest size by the standards of the DNS. As a point of comparison, the ".com" zone currently holds more than 400 million resource records {{COM-ZONE}} {{STATDNS}}, and reverse-mapping zones and those operated by hosting and content-delivery providers are also often in the hundreds of millions of resource records.

Which names exist in the zone is determined by the IANA "Autonomous System (AS)
Numbers" registry {{IANA-ASN}}, which records every allocation of a block of
ASNs to an RIR, together with the "Special-Purpose Autonomous System (AS)
Numbers" registry {{IANA-ASN-SPECIAL}}. Where each name points is determined by
the RIRs' published extended allocation and assignment reports
{{RIR-STATS}}. The procedure is specified in {{reconciliation}}.

## Reconciliation {#reconciliation}

IANA regenerates the CNAME set before each scheduled edit of the zone. Because
this is a recurring IANA work item rather than a one-time provisioning step,
this section specifies its inputs, the order in which they are applied, and the
cross-check IANA makes against the DNS.

Because deferred repointing ({{deferred}}) keeps every transferred name
resolving correctly in the interim, IANA needs only the aggregate state at
reconciliation time. No new notification path from the RIRs to IANA is required
beyond that which already exists, and none is created by this document.

In-band signaling from the RIRs to IANA is not used. Deriving the zone
from the DNS data served by an RIR would make the DNS self-referentially
authoritative for the Internet Numbers Registry System's own state.

### Inputs {#inputs}

Three inputs are used:

Which names exist:
: The IANA "Autonomous System (AS) Numbers" registry {{IANA-ASN}} specifies
  which Autonomous System Numbers are allocated to a Regional Internet Registry,
  and the "Special-Purpose Autonomous System (AS) Numbers" registry
  {{IANA-ASN-SPECIAL}} specifies which are reserved. A CNAME exists for each
  ASN which is in the first set and not in the second, and for no other ASN.

Which RIR administers each:
: The RIRs' extended allocation and assignment files state, for each ASN, which  
  RIR administers it at the time of the edit. Each
  RIR publishes a file in the NRO extended statistics exchange format
  {{NRO-STATS-FORMAT}}, and the NRO publishes the concatenation of the five
  {{RIR-STATS}}.

Why, and since when:
: The RIRs' transfer logs {{RIR-TRANSFERS}} record inter-RIR ASN transfers. Each RIR
  publishes a JSON file in the NRO transfer log format, whose "transfers" array
  carries, for each event, a "transfer_date", a "source_rir", a
  "recipient_rir", and, where Autonomous System Numbers are involved, an "asns"
  object whose "transfer_set" gives them as "start" and "end" pairs. These logs
  date and explain changes and reveal skew, but they are not individually sufficient to determine the administering RIR.

### Order of Application {#inputorder}

IANA therefore proceeds as follows:

1. Form the set of Autonomous System Numbers allocated to a Regional Internet
   Registry from {{IANA-ASN}}, and remove from it those recorded in
   {{IANA-ASN-SPECIAL}}.

2. For each ASN remaining, find the record covering it in the extended
   reports and take the administering RIR from that record's first field.

3. Emit one CNAME pointing to the ASN's label within the subdomain of that RIR.

In the event that IANA discovers a discrepancy in the course of executing this process, it leaves any existing CNAME in place and refers the discrepancy to the RIRs concerned.

### Use of the Transfer Logs {#transfercheck}

The transfer logs are examined after the CNAME set has been generated, as a check
upon it rather than as an input to it. For each inter-RIR transfer recorded
since the previous edit, IANA confirms that the extended reports now place the
ASN with the recipient RIR. Three cases arise.

* A transfer recorded in a log which the recipient's extended report does not
  yet reflect is normal and requires no action. The reports are produced daily,
  and a transfer completed since the last production run will not appear in
  them. IANA repoints the parent CNAME at the following edit, and the
  intermediate CNAME of {{deferred}} keeps the name resolving correctly
  meanwhile. IANA MUST NOT repoint on the strength of a transfer log alone.

* A change of administering RIR appearing in the extended reports with no
  corresponding transfer record is a gap in the logs, and IANA SHOULD raise it
  with the RIRs concerned. The CNAME is repointed regardless, since the
  reports govern.

* A transfer is normally recorded by both the source and the recipient RIR,
  and the two records may differ in date by up to a day where the RIRs'
  local time zones differ. IANA deduplicates on the ASN and the pair of
  RIRs, not on the date.

The logs vary within the format. Not every RIR has Autonomous System Number
transfers to report, and at the time of writing one RIR encodes the "start"
and "end" members of a "transfer_set" as JSON strings where the others encode
them as numbers. A consumer of these files accommodates both.

### Cross-Check Against the DNS {#dnscheck}

IANA SHOULD cross-check the regenerated zone against what the RIRs are
actually serving, as a check on both its own reconciliation and the RIRs'
publication. This is a read-only operation requiring no privileged access, and
it may be performed more frequently than the zone is edited.

Because an RIR zone is signed with NSEC, as required by {{denial}}, the whole
of it can be enumerated by walking the NSEC chain. Each NSEC record gives the
next name in canonical order together with the type bitmap of its own owner, so
a single pass over "arin.asn.arpa" yields every Autonomous System Number name
that RIR publishes and what it publishes there. Where an RIR offers IANA a zone transfer, a single AXFR {{RFC5936}} replaces the walk; such a transfer SHOULD be authenticated with TSIG {{RFC8945}} or carried over TLS {{RFC9103}}. The zone contents are public, so the purpose is not confidentiality but assurance that the view IANA cross-checks against is the view the RIR published. Walking all five RIR zones costs on the order of one query per published name.

The type bitmap at each Autonomous System Number name distinguishes the cases of
{{models}} and {{deferred}}:

* CNAME: the RIR has transferred the ASN away and is serving an intermediate CNAME awaiting flattening

* NS, DS: the RIR has delegated the name to the registrant

* other: the RIR is hosting the registrant's own records

* absent: the RIR publishes nothing for that ASN

IANA compares that enumeration against the zone it has generated and against the
transfer logs, and SHOULD alert the RIRs upon any of the following:

* an intermediate CNAME at an ASN for which no completed inter-RIR
  transfer is recorded, or one whose recorded recipient is not the RIR the
  CNAME points into;

* an intermediate CNAME whose target label differs from its owner label, or
  whose target lies outside "asn.arpa", contrary to {{deferred}} and
  {{models}};

* an intermediate CNAME for the same ASN in two RIRs' zones, which
  would form the loop prohibited by {{deferred}};

* an intermediate CNAME still present more than flattening cycle after IANA repointed the parent CNAME away from that RIR, contrary to {{rirconsiderations}};

* any name for an Autonomous System Number which the extended reports do not
  place with that RIR, or which is not allocated at all;

* a delegation carrying no DS RRset, where the RIR's own policy requires
  one.

Where a single ASN is in question, the chain may be checked directly, which
is the cheaper test:

    dig +norecurse +dnssec 64496.asn.arpa.      CNAME @$arpa_server
    
    dig +norecurse +dnssec 64496.arin.asn.arpa. CNAME @$arin_server

The first MUST return the CNAME IANA generated. The second returns the
intermediate CNAME of {{deferred}} during a transfer awaiting flattening, and
otherwise either the registrant's data, a delegation, or authenticated denial of
existence. Both responses are validated in the ordinary way.

## Denial of Existence {#denial}

Because the contents of the zone are public RIR data, and because the
ability to enumerate allocated Autonomous System Numbers is useful rather than
harmful, NSEC {{RFC4034}} MUST be used in preference to NSEC3 {{RFC5155}}.
RIRs MUST likewise use NSEC in the zones delegated to them, both for
the same reason and because it makes the cross-check of {{reconciliation}}
possible at the cost of a single zone walk.

A resolver may make use of NSEC Aggressive Negative Caching {{RFC8198}} to answer queries for ASNs which are not allocated or not assigned. Because only the allocated Autonomous System Numbers exist as
names, within a 32-bit space, cacheable negative gaps are wide, and a modest number of
cached records suffices to deny most queries for names that do not exist
without any of them reaching the servers of "asn.arpa" or of an RIR.

Aggressive use has a cost on the other side of a transition. A resolver
answering from a cached NSEC record sends no query, so a CNAME published by
IANA on allocation, or any data an RIR first publishes at an Autonomous System
Number name, is invisible to that resolver until the cached record expires.
Ordinary negative caching {{RFC2308}} imposes that delay on a name which was recently queried before it existed; aggressive use imposes it on every Autonomous System Number in the gap. Unlike the stale answers of {{availability}}, a synthesized denial is validly signed and a consumer cannot distinguish it from one served authoritatively, so the interval is governed entirely by the TTL of the NSEC RRset and by the SOA MINIMUM field, which {{RFC8198}} recommends that validating resolvers cap at three hours. IANA and the RIRs should choose those values short enough that the delay is tolerable to the applications described in {{applications}}, and not solely to minimize query load.

## Regional Internet Registry Considerations {#rirconsiderations}

This system requires active implementation by Regional Internet Registries, which assume the majority of the burden described here; the system is designed to minimize that burden and follow, as closely as possible, the existing RIR systems for in-addr.arpa and ip6.arpa management. An RIR which accepts a delegation under "asn.arpa" takes on a continuing but
modest set of obligations:

* Operate the delegated zone and sign it, and maintain a current DS RRset with
  IANA across key rollovers, as required by {{dnssec}}.
* Designate for that zone only nameservers named outside "asn.arpa", as
  {{rirdelegations}} requires, so that no glue is needed in the parent zone.
* For each Autonomous System Number it administers whose registrant wishes to
  participate, publish either the registrant's records or a delegation to the
  registrant, by one of the arrangements in {{models}}.
* Publish nothing at an Autonomous System Number name until the ASN has been
  assigned to a registrant and the registrant has furnished something to publish there
  ({{cnames}}).
* In conjunction with each inter-RIR ASN transfer, withdraw any records previously served at that name, publish the intermediate CNAME of
  {{deferred}}, and withdraw the CNAME at least one TTL-duration after IANA has repointed the parent (but preferably within the same flattening cycle).
* Continue to publish the extended allocation and assignment report {{NRO-STATS-FORMAT}} and the inter-RIR transfer log {{RIR-TRANSFERS}}, at the locations given in {{inputs}} and on at least the present daily schedule, on which IANA's reconciliation depends ({{reconciliation}}). An RIR that changes either location informs IANA in advance.
* Serve the delegated zone in a manner that permits the cross-check of
  {{dnscheck}}: either by signing with NSEC, as {{denial}} requires in any case,
  or by offering IANA a zone transfer.

The recurring work scales with the number of participating registrants, not
with the number of Autonomous System Numbers administered, and the provisioning
is a natural extension of the member-facing systems each RIR already
operates for reverse delegation under "in-addr.arpa" and "ip6.arpa".

## Publication Models Available to an RIR {#models}

Two publication models are permitted at "&lt;asn&gt;.&lt;rir&gt;.asn.arpa", and an RIR MAY
offer either or both, according to its own community's policy. A third is
conceivable and is prohibited.

RIR-hosted records:
: The RIR serves the registrant's records from its own signed zone,
  populated through whatever interface it offers its members. This requires no
  DNS operation on the registrant's part and keeps the entire path within a
  single signed zone.

Delegation to the registrant:
: The RIR publishes NS and DS RRsets and the registrant operates the zone.
  The zone cut falls within "asn.arpa", the chain of authentication remains
  continuous from the root, and the registrant controls publication directly.
  This suits registrants who already operate DNS infrastructure.

CNAME to a name in the registrant's own domain:
: Prohibited. An RIR MUST NOT publish a CNAME at an Autonomous System
  Number name except the transfer-intermediate CNAME of {{deferred}}, and MUST
  NOT point any CNAME at a name outside "asn.arpa".

The third, prohibited, model would re-root the authority for the data in a commercially
registered domain name, which opens the door to registration lapses and zone hijacking, and this model is also not used by RIRs in respect of their "in-addr.arpa" or "ip6.arpa" delegations.

An RIR that wishes to let a registrant publish from infrastructure the
registrant already operates should delegate the ASN label to it, which achieves the same end
without leaving the "asn.arpa" hierarchy and without extending the CNAME chain.

## Registrant Considerations

Nothing in this document requires the registrant of an Autonomous System Number
to operate a zone, to request a delegation, or to publish anything. It
is expected that many registrants, possibly most, will do nothing, and
that participation will be driven by the applications a registrant
cares about rather than by the existence of the namespace.

A registrant that does wish to publish need only choose between participating in its RIR's hosting arrangement and requesting a delegation and operating a zone
itself.

Signing is recommended but not required. This document places no requirement on
a registrant to sign a zone delegated to it, and an RIR MAY publish an insecure
delegation to a registrant that asks for one.

A registrant's participation is per-ASN. A registrant of several Autonomous
System Numbers may publish for some and not others.

The work required of registrants is the same as
they already perform for reverse delegation under "in-addr.arpa" and
"ip6.arpa". 

## What the Zone Does and Does Not Say {#absence}

The structure yields three distinguishable states for a name under
"asn.arpa":

* The ASN is not allocated to any Regional Internet Registry, or is reserved
  for a special purpose. There is no CNAME in "asn.arpa", and the zone returns
  authenticated denial of existence. The ASN is not one that any autonomous
  system should be advertising to the global routing system.

* The ASN is allocated to an RIR, but nothing is published for it. The
  CNAME exists and validates; the name it points to does not exist.

* The ASN is allocated and something is published for it. The CNAME exists
  and validates, and data is returned from the RIR side.

These are states of the zones. A resolver's view of them changes more slowly:
a transition from the first state to the second, or from the second to the
third, is not visible to a validating resolver until whatever negative
information it holds for the name expires ({{denial}}).

The first two cases both yield RCODE 3 in the final response {{RFC1034}}
{{RFC2308}}, because a CNAME chain ending at a name that does not exist is
reported as a name error for the query as a whole. The response code therefore does not
distinguish them. The distinction is carried by the
answer section: a validated CNAME from "&lt;asn&gt;.asn.arpa" is present in the
second case and absent in the first.

The second case is not further divisible from outside. Because IANA publishes
the CNAME on allocation and an RIR publishes at the target only when it has
something to publish ({{cnames}}), an ASN that has not been assigned to a
registrant and an ASN that has been assigned to a registrant who publishes
nothing produce the same result. This namespace therefore carries no indication
of whether an Autonomous System Number has been assigned. The RIRs'
published records {{RIR-STATS}}, and not the DNS, are authoritative for assignment
status.

## Availability {#availability}

The "asn.arpa" zone is served by the nameservers named in {{asnservers}},
which are, at the time of writing, the infrastructure that serves "arpa"
{{RFC9120}}. The RIRs and
registrants of Autonomous System Numbers operating zones beneath it should provision them with the
diversity and redundancy appropriate to the level of criticality of the infrastructure that the ASN identifies, and
should choose TTLs long enough that a transient server failure does not
immediately deprive consumers of data.

A resolver implementing serve-stale {{RFC8767}} may continue
answering with expired data until the authoritative servers can be reached
again. Since the data for this namespace changes rarely, serve-stale provides a useful improvement in availability. A resolver implementing {{RFC9520}} caches the
resolution failure itself, so an outage can suppress retries for a further
interval after it has ended. Neither behavior yields authenticated denial of
existence, and a consumer MUST NOT treat either as such ({{security}}).

# Privacy Considerations

Queries under "asn.arpa" reveal which autonomous system a querier is examining
and, in aggregate, may reveal a relying party's analysis. A consumer for which that exposure matters can limit it by employing QNAME minimization {{RFC9156}}, or, where an operator offers bulk retrieval of a zone, by retrieving the zone rather than querying names one at a time. Operators
of zones under "asn.arpa" should treat query logs as operationally sensitive.

# Security Considerations {#security}

The security of this namespace rests on two properties: that the name of an
autonomous system resolves, through IANA, into the zone of the RIR that
administers the ASN, and that the entire chain is signed. {{dnssec}} makes
both mandatory.

The CNAME indirection places IANA in the resolution path for every name in the
namespace. That matches the path of resource delegation, and parallels the paths used for IPv4 and IPv6 number resources: IANA
is the party that knows which RIR administers a given ASN. It does mean
that a compromise of the "asn.arpa" zone could redirect any autonomous system's
name to an attacker-controlled RIR zone, which is the same exposure that
"arpa" and the root already carry, and is addressed by the same means.

Threats to the namespace include attempts to
downgrade responses to insecure, addressed by the usual DNSSEC security measures; denial of service against the zones, addressed by
provisioning and TTL choices; and stale-but-valid data, which applications must address.

The requirement that reserved and unallocated Autonomous System Numbers return
authenticated denial of existence prevents an attacker from constructing the
appearance of a valid publication for a number that is not a legitimate
Autonomous System Number at all. That protection is the reason wildcard records are prohibited ({{cnames}}). An answer synthesized from a wildcard would still validate, so a wildcard in "asn.arpa" would replace the authenticated denial of
existence for every unallocated and reserved Autonomous System Number with
an authenticated positive answer, and one in the zone of a Regional Internet
Registry would do the same for every ASN that RIR administers but has not
assigned.

Resolution under "asn.arpa" traverses a CNAME, and during a deferred transfer
({{deferred}}) two. Resolvers limit the number of CNAME restarts they will
follow, and a resolution that exceeds the limit yields SERVFAIL, or, in older
implementations, a partial answer with a NOERROR response code. Neither outcome is
authenticated denial of existence; both are a failure to determine whether data
exists. For applications such as Digital Emblems this distinction is critical: an inability to resolve a name is not evidence that the autonomous system bears no emblem.

The "asn-servers.arpa" zone ({{asnservers}}) introduces no trust dependency of
its own. It is signed, its DS RRset is present in the "arpa" zone, and it is
validated in the same chain as everything else in this namespace. Naming the
nameservers of "asn.arpa" within "arpa" also keeps the delegation free of any
dependency on a domain administered outside the arrangements of {{RFC3172}}.

# IANA Considerations

This section is to be read as the request required by Section 3 of
{{RFC3172}}, and the IAB is asked to approve the delegations described here.

Name of the subdomain:
: "asn.arpa"

Rules for administration:
: IANA administers the "asn.arpa" zone under IAB guidance, serving it from the
  infrastructure that serves "arpa" {{RFC9120}}, and signs it with DNSSEC as required by {{dnssec}}. IANA delegates one
  subdomain to each Regional Internet Registry, each accompanied by a DS RRset,
  and publishes within the zone a CNAME record for each allocated Autonomous
  System Number pointing to the corresponding name in the subdomain of the
  RIR that administers it. The CNAME set is regenerated before each
  scheduled edit by the procedure of {{reconciliation}}, which specifies the
  inputs, their order of application, and the cross-check IANA makes against the
  DNS. Delegations are added, removed, or changed as
  Regional Internet Registries are recognized, divided, or
  derecognized through the ICANN Address Supporting Organization process
  {{ICP-2}}. Each Regional Internet Registry administers the zone delegated to
  it in accordance with the policies developed by its own community, signs it,
  and maintains the corresponding DS RRset.

Criteria for entries within the subdomain:
: The zone contains a delegation for each recognized Regional Internet
  Registry; a CNAME record for each Autonomous System Number currently
  allocated to a Regional Internet Registry, named in asplain notation as
  specified in {{cnames}}; and the records required to operate and sign the
  zone. It contains no other delegations, no names for Autonomous System
  Numbers recorded as special-purpose in the "Special-Purpose Autonomous System
  (AS) Numbers" registry {{IANA-ASN-SPECIAL}} or not allocated to a Regional
  Internet Registry, and no application data.

The same request is made in respect of the zone that names the nameservers of
"asn.arpa":

Name of the subdomain:
: "asn-servers.arpa"

Rules for administration:
: IANA administers the "asn-servers.arpa" zone under IAB guidance, delegates it
  to the same set of nameservers as "asn.arpa", installs the corresponding IPv4
  and IPv6 glue records in the "arpa" zone, and signs it with DNSSEC as
  required by {{dnssec}}. This is the arrangement {{RFC5855}} makes for
  "in-addr-servers.arpa" and "ip6-servers.arpa".

Criteria for entries within the subdomain:
: The zone contains address records for the nameservers that serve "asn.arpa",
  named as specified in {{asnservers}}, and the records required to operate and
  sign the zone. It contains no delegations and no application data.

The delegations of "in-addr-servers.arpa" and "ip6-servers.arpa" that IANA
made under {{RFC5855}} are restated by {{existingservers}} of this document and
are unchanged by it. IANA is not asked to take any action in respect of those
two zones.

IANA is further requested to record the delegations of "asn.arpa" and
"asn-servers.arpa" in its listing of the second-level domains of "arpa". No new IANA registry is created by this
document.

--- back

# Design Alternatives Considered {#alternatives}

This appendix records alternatives considered, for the working group's
information; it is expected to be removed before publication.

## Delegation of Numeric Ranges to RIRs

The obvious alternative is the structure used by "in-addr.arpa" and
"ip6.arpa", in which the parent zone delegates ranges of the numbering space
directly to the RIR that holds them. Applied to Autonomous System Numbers
this requires an encoding of the 32-bit ASN in a way that makes aggregation possible.
This alternative has been proposed before: {{I-D.ietf-dnssec-as-map}} mapped
every Autonomous System Number into "in-as.arpa" as its decimal digits in
reverse order, zero-padded to five and followed by a label giving the digit
count, so that AS 690 became "0.9.6.0.0.5.in-as.arpa". The digits were decimal
rather than binary specifically so that the boundaries of the blocks allocated
to the RIRs would fall on label boundaries. That draft addressed substantially
the present purpose, the authenticated publication of keys for autonomous
systems. It expired in 1998 and was never published, at a time when Autonomous
System Numbers in BGP were 16 bits wide, were allocated in large aligned
blocks, and were not subject to a transfer market.

### The Name is No Longer Human-Readable

Aggregation requires that the 32-bit ASN be decomposed into a hierarchy of
labels, and once it is, the name is no longer human-readable. AS 64496 becomes
"0.f.b.f.0.0.0.0.asn.arpa" under a reversed hexadecimal-nibble encoding, or
"240.251.0.0.asn.arpa" under a reversed decimal-octet encoding. Neither can be
checked by a person without a calculator, and neither
is recognizably related to AS 64496.

These names will have as much direct utility to people as to software. They
will appear in Digital Emblems and in the software that validates
them, in peering policy documents, in correspondence, and in discussion between parties disputing whether
a given autonomous system is what it claims to be. A name that must be calculated
before it can be verified will sometimes be calculated wrongly, and a
transcription error or miscalculation in this namespace would indistinguishably produce a response related to a different autonomous system.

The structure specified in {{cnames}} is the only one considered here which avoids these problems. The name of AS 64496 is "64496.asn.arpa": concise and easily related to the ASN it denotes.

### The Present Cost

A survey of the IANA registry {{IANA-ASN}} as of mid-2026 found 159 records
allocating Autonomous System Numbers to RIRs, forming 74 contiguous
single-RIR runs and covering some 140,000 ASNs. Covering those runs
requires 891 delegations under a reversed
hexadecimal-nibble encoding, or 4,626 under a reversed
decimal-octet encoding. The allocation quantum is nominally 1024
{{ASN-ALLOC-POLICY}}, but the boundaries are not aligned to it: allocations of
925 and 924 ASNs in the 32-bit space have displaced every subsequent run,
and the legacy 16-bit space is allocated at single-ASN granularity in
places, with individual ASNs held by one RIR inside runs belonging to
another.

### Each Transfer Has a Disproportionate Effect

Those figures describe IANA's block allocations, which no longer relate to the current administering RIR for each ASN. Individual Autonomous
System Numbers move between RIRs by transfer, and those movements are
recorded in the RIRs' transfer logs {{RIR-TRANSFERS}} rather than in
the IANA registry. As of mid-2026 the logs record the inter-RIR transfer of 187 individual ASNs among ARIN, RIPE, and APNIC, at a rate that has risen from one in 2018 to 32 in the first eight months of 2026. The logs are not the whole of the divergence, because they begin only in 2018. The present administering RIR must therefore be read from the RIRs' extended delegation reports {{RIR-STATS}}, which differ from IANA's block attribution for 2,098 ASNs. The figures below are accordingly computed from the extended reports, not by applying the transfer logs to the IANA registry, which would understate the fragmentation by a factor of three.

Computing the cover of the present-day ASN-to-RIR mapping raises
the number of contiguous single-RIR runs from 74 to 2,613, the exact
cover from 891 to 16,670 delegations under nibble encoding, and from
4,626 to 53,585 under octet encoding. Movement of one and a half
percent of the allocated space thus multiplies the delegation count more
than eighteenfold, because each ASN removed from the interior of an
aggregate shatters it into aligned fragments. Moving one further ASN,
drawn at random from the present distribution, costs approximately 25
additional delegations.

### The Cost Increases Over Time

Transfers are driven by corporate restructuring and a
market in number resources. Each transfer is individually rational,
independent of every other, and unconstrained by numeric adjacency. No party acquiring
a company or an ASN has any reason to prefer one whose Autonomous System
Number would preserve aggregation, and the market does not facilitate aggregation-preserving transactions.

Unlike IP addresses, the disaggregation of ASNs has no inverse mechanism. There is no party in a position to re-aggregate ASNs: IANA cannot renumber an autonomous system and an RIR cannot compel a registrant to exchange its ASN for a numerically convenient one. Every transfer therefore increases fragmentation permanently,
and no mechanism exists by which fragmentation can decrease.

It follows that the present state of aggregation is the tidiest that will ever
be observed. Every future state is more fragmented than its predecessors,
and the distribution of ASNs across RIRs is driven by entropy toward a
stochastic state: an arbitrary mapping from a 32-bit ASN onto one of five or more
RIRs, with no residual structure from which to derive compression. A
range-delegation design would therefore function best on the day it was
specified and would degrade from that day onward, with the "asn.arpa" zone
absorbing on the order of 25 further delegations for every autonomous system
that changes region, indefinitely.

Moreover, a delegation model would require that IANA immediately reflect each
inter-RIR transfer, increasing its workload from roughly five simple
actions per year to more than fifty at the present transfer rate, and to an
unbounded larger number in years to come.

The structure specified in {{cnames}} is unaffected by these problems. Its cost
is one record per allocated ASN, regardless of the distribution of those ASNs
across RIRs, a transfer changes one record rather than fragmenting a
delegation, and the IANA work is done at the IANA's convenience rather than in response to market actions.

### Projection

The two structures were projected forward from the present state. New IANA
allocation was modeled at 5,120 ASNs per year, the mean of 2015 through
2026 {{IANA-ASN}}, apportioned among the RIRs in their recent shares and
appended to each RIR's existing run. The allocations from 2018 to 2026 have a very nearly linear slope.

New allocation by IANA imposes negligible fragmentation cost. If one ignores the effect of transfers, when IANA appends a block to the end of an RIR's existing run the number of single-RIR runs remains at roughly 2,620 and the nibble cover at roughly 16,900 indefinitely, even as the allocated space grows from 140,000 ASNs to 263,000. Fragmentation results from transfers rather than new allocations.

Under a range-delegation design, about nine resource records are necessary to represent each delegation. Under a CNAME structure, four. Projecting the increase in allocations forward yields the following growth under each model:

          allocated  cumulative              delegation     CNAME
    year       ASNs  ASN moves  delegations  model RRs  model RRs  ratio
    2026    140,286      2,098       16,670    150,030    561,144    3.7
    2030    160,770      2,342       22,212    199,908    643,080    3.2
    2040    211,980      3,367       40,565    365,085    847,920    2.3
    2050    263,190      4,984       64,532    580,788  1,052,760    1.8

The number of resource records in the zone continues to favor the delegation model for several decades hence, but the number of resource records is inexpensive relative to the complexity of the work involved, particularly for IANA. It is that difference in workload, rather than zone size, that recommends the CNAME method. A CNAME is unilaterally asserted and mechanically generated from RIR data. A delegation is a bilateral relationship between parties, requiring nameserver
designation, glue where applicable, a DS RRset, and coordination of that DS
RRset with the child across every key rollover forever. Five such arrangements are tractable. The 16,670 which would be required today and more than 22,000 four years from now represent an infeasible additional workload for IANA and the RIRs.

Deferred repointing ({{deferred}}) further strengthens the argument in favor of CNAMEs. Under the structure specified here, IANA's annual operations on "asn.arpa" occur during its allocation operations, some five a year, regardless of how many ASNs change region, and are automated, requiring no interaction with RIR personnel. A range-delegation design cannot do the same. An RIR could in principle defer a transfer by delegating the fragment onward with NS records, but that requires the source RIR to hold a DS RRset for the recipient RIR's key inside
its own zone, and it relocates the fragmentation into the RIRs' zones rather than eliminating it. When IANA eventually reconciles, the edit still touches on the order of twenty-five delegation records for each transferred ASN, against one automated CNAME repoint.

Range delegation also increases complexity in other ways: for instance, an ASN moving out of the interior of another RIR's range requires either that the RIR holding the covering range serve a name on the recipient RIR's behalf, or that IANA publish a more-specific delegation that contradicts the covering one.