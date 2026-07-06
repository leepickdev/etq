# Security

## Verifying releases

Every release is signed. The release signing public key has this SHA-256
fingerprint — cross-check it against the copies published at
https://etiquekit.com/docs/ and in the npm package README before trusting a
downloaded key:

```
917fbced1d6a82897ec3441a1d12947803ca4d42a6bc63d3412dee8bf8c3ce31
```

Verify any artifact:

```sh
curl -fsSLO https://etiquekit.com/releases/SHA256SUMS
curl -fsSLO https://etiquekit.com/releases/SHA256SUMS.sig
curl -fsSLO https://etiquekit.com/releases/etiquette-release-signing.pub.pem
shasum -a 256 etiquette-release-signing.pub.pem   # must match the fingerprint above
openssl dgst -sha256 -verify etiquette-release-signing.pub.pem \
  -signature SHA256SUMS.sig SHA256SUMS
shasum -a 256 -c SHA256SUMS
```

The artifacts attached to GitHub Releases here are the same signed bytes; the
npm registry serves them byte-identically (compare against `SHA256SUMS`).

## Reporting a vulnerability

Use GitHub's private vulnerability reporting on this repository
(Security → Report a vulnerability). Do not open public issues for
security reports. If a downloaded artifact fails signature verification,
stop, do not install, and report it the same way.
