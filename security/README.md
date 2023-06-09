In the near future, Violet Moon mods will start to have `.asc` GPG signatures generated at
release time.

These signatures will be signed by the ED25519 private key with fingerprint
`C55FFFF9E4E4C0C09AB04B7C704178B3439DADC3`. The corresponding public key is located
adjacent to this file in [`SIGNING_PUBLIC_KEY.txt`](./SIGNING_PUBLIC_KEY.txt).

When releases are made, we will try to convey the `.asc` signatures alongside any release
announcements such as announcements on the mailing list, attaching them to the GitHub
release tag, etc. We are new to doing this and not all processes have been put in place
yet, so please bear with us.

To verify that a given JAR was produced by the signing key mentioned above, you can do the
following on a Unix shell with curl and GPG:

```
$ curl https://raw.githubusercontent.com/VazkiiMods/.github/main/security/SIGNING_PUBLIC_KEY.txt | gpg --import
$ gpg --verify Neat.jar.asc Neat.jar
gpg: Signature made Fri 09 Jun 2023 01:09:48 AM PDT
gpg:                using EDDSA key C55FFFF9E4E4C0C09AB04B7C704178B3439DADC3
gpg: Good signature from "Violet Moon Signing Key" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: C55F FFF9 E4E4 C0C0 9AB0  4B7C 7041 78B3 439D ADC3
```

The warning at the end is GPG saying "Yes, this public key C55F... created the
signature. But it can't be proven that this public key is actually the real 'Violet Moon
Signing Key'".

This document, uploaded to Violet Moon's GitHub organization, proves that last gap.
