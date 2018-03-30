# SSL Certificates

Having an SSL certificate for a domain allows to use HTTPS instead of HTTP for the application that is pointed to by this domain.

## How to create an SSL certificate and private key for a domain

Use the following:

- [Let's Encrypt](https://letsencrypt.org/): a free certificate authority.
- [Certbot](https://certbot.eff.org/): a tool for verifying domain ownership and creating Let's Encrypt-signed certificates and private keys.

This solution is completely free.

### Steps

1. Log in to the machine that the desired domain points to (you must have set up DNS records already).
2. Make sure that port 80 is free on this machine (if you don't use one of the supported web servers listed on <https://certbot.eff.org/>)
3. Follow the instructions on <https://certbot.eff.org/lets-encrypt/ubuntuxenial-other> (select software and OS appropriately).
4. If everything works, certbot creates and saves the certificate and private key as `.pem` files on the local file system.

### Notes

On a given host, you can only create a certificate for the domain that actually resolved to this host.

For example, if domain `sent2vec.quantumsense.ai` resolves to host `A`, then, on host `A`, you can only create a certificate for `sent2vec.quantumsense.ai`, but not for e.g. `quantumsense.ai`. For creating a certificate for `quantumsense.ai`, you have to execute the above procedure on the host to which `quantumsense.ai` points.

## Security

The private key files in this repository are encrypted with PGP using [git-secret](https://github.com/sobolevn/git-secret).
