## Notes on certificate pinning 

August 2014 - Certificate pinning is really effective to prevent man-in-the-middle attacks. Chrome has gotten very successful results, but unfortunately, scaling certificate pinning is difficult. The current technique involves manual verification by the Chrome Security Team before adding a description of the signing chain to the Chromium source. Three researchers from the CST worked on a IETF proposal to make scale certificate pinning. The system is TOFU and uses a new HTTP header to notify the client that he should pin a specific certificate chain. It is meant to be used along with HSTS to enforce HTTPS connections with that website. The implementation relies on pinning of SHA256 of the public key. A “max-age” property allows to specify for how long a host should be considered as a “known pinned host”. A pinning policy can also be given for subdomains. The risks involved in the deployment are to make websites inaccessible due to invalid/inconsistent browser data. 

A notable feature of this proposal is the fact that a ‘report-uri’ can be specified. If present, the client will report pinning failures to the specified server. I think this could be used as an attack vector. Indeed, if you consider that the attacker can spoof DNS entries for instance, he can prevent a client from reporting an attack. ‘report-uri’ may be a HTTP or HTTPS host and does not have to be on the same Internet domain. When verification of a pin fails, a JSON is posted to the ‘report-uri’ (see RFC for format).

Pins are elaborated on public keys in chain. But no way to blacklist a specific key? How can I upgrade the Pin for my users not to be vulnerable to attacks using my old key?

Another concern is related to how Pinning can be effective with ephemerality. The Tor Browser Bundle clears state after being used for anti-forensics reasons. That would prevent pinning to be effective since a new pin will always be set on a “per exit-node” basis.

