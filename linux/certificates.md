# Certificates

Jamie says it all much better than me...

  * [Create a root certificate](https://jamielinux.com/docs/openssl-certificate-authority/create-the-root-pair.html)
  * [Create private key (or CSR)](https://jamielinux.com/docs/openssl-certificate-authority/sign-server-and-client-certificates.html)

# Sign the key (or CSR)

```
cd /root/ca
openssl ca -config intermediate/openssl.cnf \
      -extensions server_cert -days 375 -notext -md sha256 \
      -in intermediate/csr/www.example.com.csr.pem \
      -out intermediate/certs/www.example.com.cert.pem
chmod 444 intermediate/certs/www.example.com.cert.pem
```

openssl ca -config intermediate/openssl.cnf -extensions server_cert -days 375 -notext -md sha256 -in intermediate/csr/www.example.com.csr.pem -out intermediate/certs/www.example.com.cert.pem

# Create certificate with full chain
```
cat intermediate/certs/ca-chain.cert.pem >> yourcertificate.pem
```

This appends the chain to the cert
