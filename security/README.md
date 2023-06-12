Violet Moon mods will start to have `.asc` GPG signatures generated at
release time. These signatures will be signed by the ED25519 private key with fingerprint
`C55FFFF9E4E4C0C09AB04B7C704178B3439DADC3`. The corresponding public key is located
adjacent to this file in [`SIGNING_PUBLIC_KEY.txt`](./SIGNING_PUBLIC_KEY.txt).

When releases are made, we will try to convey the `.asc` signatures alongside any release
announcements such as announcements on the mailing list, attaching them to the GitHub
release tag, etc. We are new to doing this and not all processes have been put in place
yet, so please bear with us.

To verify that a given JAR was produced by the signing key mentioned above, you can do the
following on a Unix shell with curl and GPG:

```bash
# Only need to do this once
$ curl https://raw.githubusercontent.com/VazkiiMods/.github/main/security/SIGNING_PUBLIC_KEY.txt | gpg --import

# Verify a signature
$ gpg --verify <the asc file> <the jar file>
gpg: Signature made Fri 09 Jun 2023 01:09:48 AM PDT
gpg:                using EDDSA key C55FFFF9E4E4C0C09AB04B7C704178B3439DADC3
gpg: Good signature from "Violet Moon Signing Key" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: C55F FFF9 E4E4 C0C0 9AB0  4B7C 7041 78B3 439D ADC3
```
You want to make sure that it says "Good signature", and that the primary key fingerprint shown
matches the one I mentioned above in the first paragraph (spaces don't matter).

If you see both of those you can, with pretty strong confidence, trust that the JAR file
was created and released by the Violet Moon developers.

NOTE: The warning at the end is GPG saying "Yes, this public key C55F... created the
signature. But it can't be proven that this public key is actually the real 'Violet Moon
Signing Key'".

This document, uploaded to Violet Moon's GitHub organization, proves that last gap.

## But what if your private key gets stolen?
We're using GitHub actions' [encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) to store the private key.
This means the key is never actually present on any developer's machine (in fact, you can't get it back out of the encrypted secrets page after you put it in).

If GitHub gets compromised and leaks the key, the world will have much much bigger problems. Of course, a developer can still push malicious code, but
we are relying on the open source model to keep us honest here.

## What if a jar is infected locally?
The uploading of releases happens entirely in GitHub actions. Developers do not need to download and submit the files themself.
As above, the only time this will actually be a problem is if GitHub itself is compromised.
