# 🌐 ACME Certificate Flow: High-Level Overview

\


The ACME (Automatic Certificate Management Environment) protocol automates the process of domain validation and certificate issuance. Here’s the general back-and-forth flow:

***

Client registers with Certificate Authority (CA)

* The ACME client (like Traefik, Certbot, etc.) contacts the ACME server (e.g., Let’s Encrypt).
* It registers an account with an email and a public key (used to authenticate future requests).

***

#### Client requests a certificate

*   The client says:

    > “I want a TLS certificate for example.com (and maybe www.example.com).”

***

#### CA responds with a challenge

*   The CA replies:

    > “Prove you control example.com by completing one of the following challenges.”

\


There are three common types:

* HTTP-01 — Serve a file at http://example.com/.well-known/acme-challenge/XYZ
* DNS-01 — Add a DNS TXT record under \_acme-challenge.example.com
* TLS-ALPN-01 — Serve a special certificate over TLS using ALPN (less common)

***

#### Client fulfills the challenge

* The client does what the CA asks — adds the file or DNS record, for example.
* This step is automated in most tools.

***

#### CA verifies the challenge

* The CA checks:
  * For HTTP-01: Can it download the file from the domain?
  * For DNS-01: Can it query the correct TXT record from the domain’s DNS?
* If validation passes, it moves on.

***

#### Client requests certificate issuance

*   The client says:

    > “Okay, I proved ownership. Now please sign this Certificate Signing Request (CSR).”

\


The CSR includes:

* The domain(s)
* The client’s public key
* Optional metadata

***

#### CA issues the certificate

* The CA signs and returns a valid X.509 certificate, proving the domain is secure and trusted.
* This cert is valid for 90 days (in Let’s Encrypt’s case).

***

#### Client installs and uses the cert

* The client stores and uses the cert — often with automatic renewal built in.
* Your server can now serve HTTPS traffic using the certificate.

***

#### Renewal cycle

* The client regularly renews the cert (typically \~30 days before expiry) by repeating the challenge and request.
