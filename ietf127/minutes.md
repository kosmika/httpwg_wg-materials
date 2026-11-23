# IETF127 HTTP Working Group Minutes

Scribe: Mike English

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Resumable Uploads for HTTP](#resumable-uploads-for-http)
- [Cookies: HTTP State Management Mechanism](#cookies-http-state-management-mechanism)
- [The Preliminary Request Denied HTTP Status Code](#the-preliminary-request-denied-http-status-code)
- [Secondary Certificate Authentication of HTTP Servers](#secondary-certificate-authentication-of-http-servers)
  - [PR #3584 - Client-only SETTINGS negotiation](#pr-3584---client-only-settings-negotiation)
  - [PR #3586 - Certificate errors](#pr-3586---certificate-errors)
  - [PR #3585 - Trust store divergence](#pr-3585---trust-store-divergence)
  - [Issue #3590 - Authority and scope](#issue-3590---authority-and-scope)
  - [Issue #3497 - Rename SERVER_CERTIFICATE](#issue-3497---rename-server_certificate)
- [HTTP Signature-Key Header](#http-signature-key-header)
- [The Redirect-By HTTP Response Header Field](#the-redirect-by-http-response-header-field)
- [Guidance on the 402 (Payment Required) Status Code](#guidance-on-the-402-payment-required-status-code)
- [Parallel Appends for Resumable Uploads](#parallel-appends-for-resumable-uploads)
- [Authenticating HTTP Tunnels with HTTP Message Signatures](#authenticating-http-tunnels-with-http-message-signatures)
- [Unbound DATA for CONNECT in HTTP/3](#unbound-data-for-connect-in-http3)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Resumable Uploads for HTTP

Document: 
https://datatracker.ietf.org/doc/draft-ietf-httpbis-resumable-upload/

Slides:
https://datatracker.ietf.org/meeting/127/materials/slides-127-httpbis-resumable-uploads-00

Plan to cut one more draft and then go to standard 2 week WGLC

## Cookies: HTTP State Management Mechanism

not present: will ask for update on list

## The Preliminary Request Denied HTTP Status Code

one user of this status code, may be a workaround for the conflict

419 looks good

Ready for WGLC?

## Secondary Certificate Authentication of HTTP Servers

Eric Gorbaty presenting

Document:
https://datatracker.ietf.org/doc/draft-ietf-httpbis-secondary-server-certs/

Slides:
https://datatracker.ietf.org/meeting/127/materials/slides-127-httpbis-secondary-certificate-authentication-of-http-servers-00

### PR #3584 - Client-only SETTINGS negotiation

no objects raised at mic

MT in chat: "no optional and useless stuff, please. But I don't care enough to stand up."

### PR #3586 - Certificate errors

BenS: supports keeping

chat: Nitin Tak "+1 Ben"

ErikN: ... (additional fingerprinting vector?)

BenS: not necessarily

chat Lucas Pardue: "I can't get to the mic, but I think this makes sense to keep". maybe provide option, but not encourage

resolution: Eric to update PR

### PR #3585 - Trust store divergence

Alessandro: why do we need to say anything about this?

MT: +1 Alessandro, it's OK to have different trust store decisions. Recommend cutting the SHOULD text.

Resolution: close PR to change

### Issue #3590 - Authority and scope

Alessandro: Don't talk about TLS session resumption in HTTP

MT: agreeing with Alessandro to a degree, but we probably do want to say something here

Resolution: tighten language around existing connection scope and leave it at that

### Issue #3497 - Rename SERVER_CERTIFICATE

no objections to keeping the current name and closing the issue

PTTH chair is happy to be present in the reverse PTTH WG today

BenS: mentioning similarity to ECH fine, mentioning some ways fine, trying to enumerate them all, probably not

## HTTP Signature-Key Header

call for adoption on list failed, this is discussion following up on that

Document:
https://datatracker.ietf.org/doc/draft-hardt-httpbis-signature-key/

Slides:
https://datatracker.ietf.org/meeting/127/materials/slides-127-httpbis-http-signature-keys-01

Joost: should parts of this happen in different places?

MT: ...

Justin: ... different places may have different semantics

Ted: may be useful to see if there are common threat models even if there aren't common semantics

Will sync w/ other groups and come back here if it seems useful

## The Redirect-By HTTP Response Header Field

Joost de Valk

Doc:
https://datatracker.ietf.org/doc/draft-devalk-redirect-by/

Slides:
https://datatracker.ietf.org/meeting/127/materials/slides-127-httpbis-redirect-by-00

Widely deployed X-Redirect-By never standardized, this small doc is for doing that now as Redirect-By.

Thom Vaughan: existing deploy base has different levels of specificity. Is there a particular level in mind, or left up to implementations?
    - granular is good 

BenS: If the only thing you can do with this is nothing, maybe it should be called "Comment:" Would love a "Comment:" header.

MarkN (no hats): mixed feelings, has experience trying to standardize common paths, not a lot of pressure for adoption, should manage expectations. Unlikely existing implementations will change unless there's something that starts processing this information and provides incentives to change... but that would be developing a new protocol and would require further discussion.

Mike Bishop (no hats): agree with Mark, similar to error strings - reader is the person who generated it - "note to self"

Joost: own implementation is probably biggest current user, so there is a chance things would be updated

Justin Richer: should allow for multiple values of this header

Mark: status code / redirect happens only once, how would there be more?

Justin: comment idea

Mark: not sure that's actually on the table

Shocking revelation: Mark doesn't think that ever field should be a structured field. It is Friday.

Show of hands: Are you interested in pursuing this work?
* total participants 75
* yes 11
* no 1
* no opinion 21


## Guidance on the 402 (Payment Required) Status Code

Doc:
https://datatracker.ietf.org/doc/draft-nottingham-httpbis-402/

Slides:
https://datatracker.ietf.org/meeting/127/materials/slides-127-httpbis-402-payment-required-00

Proposal: define status code semantics to allow this use

Ted: If someone asks for "three Haily Marys" does that fit?

Mark: probably true of most status codes

Ted: Not sure if it's useful to say that you don't know what things mean unless you emitted them

Mark: harm trying to guard against is people squatting on this code

DavidS: history seems to trace back to 1997 - does anyone remember _why_ it was reserved for this purpose?
    - unclear

MT: Is there a risk of conflicting mechanisms here?

Mark: question is whether we have the will to address that in this WG

MT: probably useful to at least call out the hazard in this draft

Mark: makes sense

Erin Simon: does 412 already encompass this?

Mark: precondition is a specific term of art in HTTP and different than this

Tommy Pauly: worthwhile to also provide guidance on how implementations could co-exist?

Mark: yes

DavidS: if problem is that people are using code point and it's not working, how does this document fix it?

Mark: gets us out of the way by clarifying the status of the status code

DavidS: could we instead deprecate it?

Mark: that wouldn't face reality of current use

Show of hands: Are you interested in adopting this document (on 402) in this WG?

* total participants 75
* yes 15
* no 3
* no opinion 18

Any of the no's want to say more? (No)

## Parallel Appends for Resumable Uploads

Slides:
https://datatracker.ietf.org/meeting/127/materials/slides-127-httpbis-parallel-appends-for-resumable-uploads-00

Doc:
https://datatracker.ietf.org/doc/draft-spk-httpbis-parallel-upload/

DavidS: you've convinced me that you "could" not necessarily that you "should"
    - transport protocols have gotten much better and smarter
    - two connections being faster that one points to a bug in your transport protocol
    - ...
    - focusing on parallel streams in one connection..
    - still have same congestions controller and same overall throughput, what is gained?
    - ...
    - taking offline

(note: lots of discussion in chat)

Marius Kleidl: small reorder window could cause some overhead

MT relaying Lucas from chat: why do people assume that the HTTP client source is one device?

MT: this will require a lot of justification, may be other approaches


## Authenticating HTTP Tunnels with HTTP Message Signatures

Document:
https://datatracker.ietf.org/doc/draft-rosomakho-httpbis-tunnels-signatures/

Slides:
https://datatracker.ietf.org/meeting/127/materials/slides-127-httpbis-authenticating-http-tunnels-with-http-message-signatures-00

Flemming: supports this work

DavidS: overall in support of ways of authenticating tunnels, this seems good, can concealed tunnels work with this?

Yaroslav: If you try hard enough... But would require significant additional work

BenS: ... there are so many slightly better solutions. not trying to reinvent HTTP message signatures

Ben would love to see an authentication scheme that is "signature"

Jim: endorses this

Arndt: benefit of using signatures is that it generalizes

Justin: ... (scribe: context on why other things don't quite work, I think?)

(see also chat discussion)

Resolution: will continue discussion and talk to wimse chairs

## Unbound DATA for CONNECT in HTTP/3

Slides:
https://datatracker.ietf.org/meeting/127/materials/slides-127-httpbis-unbound-data-if-time-allows-00

Doc:
https://datatracker.ietf.org/doc/draft-rosomakho-httpbis-h3-unbound-data/

ask: adopt? OK if experimental

BenS: happy to see this move forward in whatever category

Mike Bishop (no hats): this was originally in H3 and was pulled out, not bad to bring it back as an extension

Alessandro: questions: difference between unbound and handoff?
    - makes more difference with certain libraries, not so much with CF quiche

Alessandro: happy for this to continue, experimental seems pointless, can be a real thing

Talk to chairs if experimental category is important to support for adoption, otherwise will take to list
