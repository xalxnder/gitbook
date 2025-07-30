# Certificates

## What is a Certificate?

A **certificate** (specifically an **SSL/TLS certificate**) is a digital file that verifies the identity of a website and enables encrypted communication between a client (like your browser) and a server. It ensures that data is transmitted securely and protects against attackers intercepting sensitive information.

## TLS vs SSL

TLS (Transport Layer Security) and SSL (Secure Sockets Layer) are both cryptographic protocols designed to secure communication over a network. However, TLS is the modern, more secure version of SSL. Even though SSL is outdated, people still use “SSL” as a general term for encrypted communication. However, when setting up security (like in Traefik or Cert-Manager), you’re actually using **TLS**.

## Lets Encrypt

The objective of Let’s Encrypt and the [ACME protocol](https://tools.ietf.org/html/rfc8555) is to make it possible to set up an HTTPS server and have it automatically obtain a browser-trusted certificate, without any human intervention. This is accomplished by running a certificate management agent on the web server.

Let’s Encrypt’s ACME (Automatic Certificate Mangement Environment) protocol defines how clients communicate with its servers to request certificates, verify domain ownership, and download certificates. It is currently in the process of becoming an official [IETF](https://www.ietf.org/) standard.

Let’s Encrypt offers _**domain-validated**_**&#x20;certificates**, meaning they have to check that the certificate request comes from a person who actually controls the domain. They do this by sending the client a unique token, and then making a web or DNS request to retrieve a key derived from that token.

For example, with the HTTP-based challenge, the client will compute a key from the unique token and an account token, then place the results in a file to be served by the web server. The Let’s Encrypt servers then retrieve the file at `http://==example.com==/.well-known/acme-challenge/==token==`. If the key is correct, the client has proven it can control resources on `==example.com==`, and the server will sign and return a certificate.
