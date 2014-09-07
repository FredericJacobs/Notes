# GNS - The GNU Name System

## Motivation

DNS was not designed with security in mind. DNSSEC extensions are meant to fix the issue but come with their own problems in addition to the weaknesses of the DNS system (hierarchical, lack of query privacy …) like the use of RSA that leads to very long packet sizes, compel of DNS authorities to manipulate entries and certify the changes.

## Design goals 

GNU is a **censorship-resistant**, **privacy-preserving** and **decentralized name system** designed to provide a secure alternative DNS. The foundation of the GNS system is a pet name system, where each individual user may freely and securely map names to values. If we refer to Zooko’s triangle, GNS has chosen the secure and memorable but left out the globally unique property. A domain owner can securely delegate a subdomain to another user thanks to SDSI/SPKI. A DHT is at the core of GNS to distribute the key-value mappings. 

## Adversary model

Adversary modelled after a state trying to limit access to information. We allow adversary to participate in any role in the name system. Computationally, the adversary is allowed to have more resources than all benign users combined. It is assumed that all the communications between GNS participants are unhindered.

## Notes on SDSI/SPKI

SDSI/SPKI is a merger of the Simple Distributed Security Infrastructure and the Simple Public Key Infrastructure. It defines a public-key infrastructure that abandons the concept of memorable global names and does not require certification authorities. SDSI/SPKI has the central notion of principals which are globally unique public keys.

## Names, Zones and Delegations 

GNS names are public keys. Namespaces constitute the zones in GNS, a zone is a public-private key pair and a set of records. GNS records consist of a label, type, value and expiration time. Labels have the same syntax as in DNS. 

## Primitives 

GNS relies on ECC, namely ECDSA on Curve25519.

## Conclusion

I think GNS is interesting as a temporary solution for tech-savvy who want to have a decentralized secure naming-system. The lack of unique naming scheme makes it terribly confusing and I’m not yet convinced that this really protects against more advanced social engineering attacks. Certificate pinning is definitely the way to go but it’s still unclear how the mapping can be done. Blockchains might be the solution but the ridiculous consumption of the proof of work algorithms, the 51% attacks, and squatting issues are preventing mainstream adoption of things like Namecoin.

## More 

Read more in the “A Censorship-Resistant, Privacy-Enhancing and Fully Decentralized Name System” paper by Matthias Wachs, Martin Schanzenbach, Christian Grothoff.
