# ci-automation-client

DID used by **CI and automated security tests** (e.g. GitHub Actions for `platform-core`). Do not use this identity in production user apps.

**Private key:** store only in GitHub Actions secret `TRUGANIC_CI_CLIENT_PRIVATE_KEY` (hex). The matching public key is in `did.json`.

After changing keys, update the secret and this `did.json`, then publish to the hosted `did-documents` site so `did:web` resolution works.
