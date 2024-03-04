# multi-ingress-repro
Reproduction of race condition issue with nginx secret annotations

Generated a cert for `proxy_ssl_secret.yaml` with `openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 365 -nodes -subj "/C=XY/O=Whatever/OU=Whatever/CN=host-1.does.not.matter"`.

As you can see reproduction does not require that the certificate be valid for the hostname, just that it is a valid certificate. I tried providing some gibberish base64-encoded data as the secret-data but could not reproduce the issue.

Note the ingresses need not be functional. E.g. need not direct traffic to an extant service.

Note helm will always install Secrets before Ingresses.