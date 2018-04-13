# SSL Certificates

Having an SSL certificate for a domain allows to use HTTPS instead of HTTP for the application that is pointed to by this domain.

## How to create an SSL certificate and private key for a domain

Use the following:

- [Let's Encrypt](https://letsencrypt.org/): a free and automated certificate authority.
- [Certbot](https://certbot.eff.org/): an [ACME](https://en.wikipedia.org/wiki/Automated_Certificate_Management_Environment) client (for automated domain validation and certificate issuance).

This solution is completely free.

### Steps

1. Log in to the machine that the desired domain points to (you must have set up DNS records already).
2. Make sure that port 80 is free on this machine (if you don't use one of the supported web servers listed on <https://certbot.eff.org/>)
3. Follow the instructions on <https://certbot.eff.org/lets-encrypt/ubuntuxenial-other> (or select software and OS appropriately).
4. If everything works, certbot creates and saves the certificate and private key as `.pem` files under the directory `/etc/letsencrypt/live` on the local file system.

### Notes

On a given host, you can only create a certificate for the domain that actually resolved to this host.

For example, if domain `sent2vec.quantumsense.ai` resolves to host `A`, then, on host `A`, you can only create a certificate for `sent2vec.quantumsense.ai`, but not for e.g. `quantumsense.ai`. For creating a certificate for `quantumsense.ai`, you have to execute the above procedure on the host to which `quantumsense.ai` points.

## Security

The private key files in this repository are encrypted with PGP using [git-secret](https://github.com/sobolevn/git-secret).


## Other ways to get free SSL certificates

[AWS Certificate Manager (ACM)](https://aws.amazon.com/certificate-manager/) allows to create free SSL certificates as well. However, these certificates can only be used within AWS, and only for specific AWS services.

Currently, the services for which ACM-generated certificates can be used include (see [here](https://aws.amazon.com/certificate-manager/faqs/)):

- Elastic Load Balancing
- Amazon CloudFront
- Amazon API Gateway
- AWS Elastic Beanstalk
- AWS CloudFormation

ACM-generated certificates cannot be used outside of AWS. In particular, it is possible to export the certificate, but it is not possible to export the corresponding private key (see [here](https://docs.aws.amazon.com/acm/latest/userguide/acm-certificate.html) and [here](https://www.reddit.com/r/aws/comments/5ov7rd/acmkms_is_it_possible_to_obtain_the_private_key/)).
