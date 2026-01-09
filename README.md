# TruGanic DID Documents

A comprehensive repository of Decentralized Identifier (DID) documents for the TruGanic ecosystem. This repository contains DID documents for various actors in the TruGanic supply chain network, including farmers, transport agents, certification bodies, and AR/ML services.

## Table of Contents

- [Overview](#overview)
- [What are DIDs?](#what-are-dids)
- [Repository Structure](#repository-structure)
- [DID Method](#did-method)
- [Client DIDs](#client-dids)
- [Server DIDs](#server-dids)
- [Cryptographic Templates](#cryptographic-templates)
- [Usage](#usage)
- [Configuration](#configuration)
- [Deployment](#deployment)
- [Security Considerations](#security-considerations)
- [Contributing](#contributing)

## Overview

This repository hosts DID documents for the TruGanic platform, enabling decentralized identity management across the supply chain. Each actor in the TruGanic ecosystem has a unique DID that can be used for authentication, verification, and establishing trust relationships.

## What are DIDs?

Decentralized Identifiers (DIDs) are a new type of identifier that enables verifiable, decentralized digital identity. A DID is a URI that:

- Points to a DID document containing cryptographic material and other metadata
- Is controlled by the entity it identifies (self-sovereign identity)
- Can be resolved to a DID document without relying on a centralized registry
- Enables cryptographic verification of interactions

For more information, see the [W3C DID Specification](https://www.w3.org/TR/did-core/).

## Repository Structure

```
did-documents/
├── core/                    # Core DID document for the TruGanic platform
├── clients/                 # Client-side DID documents
│   ├── ar-ml-client/
│   ├── certification-body-client/
│   ├── demo-client-1/
│   ├── farmer-client/
│   └── transport-agent-client/
├── servers/                 # Server-side DID documents
│   ├── ar-ml-server/
│   ├── certification-body-server/
│   ├── demo-server-1/
│   ├── demo-server-2/
│   ├── farmer-server/
│   └── transport-agent-server/
└── templates/               # Cryptographic algorithm templates
    ├── Ed25519/
    ├── ES256 (P-256)/
    ├── ES256K (secp256k1)/
    ├── ES384 (P-384)/
    ├── ES512 (P-521)/
    └── RS256 (RSA)/
```

## DID Method

This repository uses the **`did:web`** method, which allows DIDs to be resolved from well-known locations on the web. The DID format follows this pattern:

```
did:web:truganic.github.io:did-documents:{category}:{entity-name}
```

### Example

```
did:web:truganic.github.io:did-documents:clients:farmer-client
```

This DID resolves to:

```
https://truganic.github.io/did-documents/clients/farmer-client/did.json
```

## Client DIDs

Client DIDs are used by end-user applications and services that interact with the TruGanic platform. Each client has its own DID document for authentication and verification purposes.

### Available Client DIDs

- **`farmer-client`** - DID for farmer client applications
- **`transport-agent-client`** - DID for transport agent client applications
- **`certification-body-client`** - DID for certification body client applications
- **`ar-ml-client`** - DID for AR/ML client applications
- **`demo-client-1`** - Demo client for testing purposes

### Client DID Structure

Each client DID document includes:

- **`@context`**: W3C DID context
- **`id`**: The DID identifier
- **`verificationMethod`**: Cryptographic keys for verification
- **`authentication`**: Methods used for authentication

## Server DIDs

Server DIDs are used by backend services and APIs in the TruGanic ecosystem. These DIDs enable server-to-server authentication and verification.

### Available Server DIDs

- **`farmer-server`** - DID for farmer backend services
- **`transport-agent-server`** - DID for transport agent backend services
- **`certification-body-server`** - DID for certification body backend services
- **`ar-ml-server`** - DID for AR/ML backend services
- **`demo-server-1`** - Demo server for testing purposes
- **`demo-server-2`** - Additional demo server for testing

### Server DID Structure

Server DID documents follow the same structure as client DIDs, with server-specific cryptographic keys and authentication methods.

## Cryptographic Templates

The `templates/` directory contains example DID documents for different cryptographic algorithms. These templates can be used as references when creating new DID documents.

### Supported Algorithms

1. **Ed25519** (`Ed25519/`)

   - Curve: Ed25519
   - Key Type: OKP (Octet Key Pair)
   - Use case: Fast, efficient signatures

2. **ES256** (`ES256 (P-256)/`)

   - Curve: P-256 (secp256r1)
   - Key Type: EC (Elliptic Curve)
   - Use case: Widely supported ECDSA signatures

3. **ES256K** (`ES256K (secp256k1)/`)

   - Curve: secp256k1
   - Key Type: EC (Elliptic Curve)
   - Use case: Bitcoin-compatible signatures

4. **ES384** (`ES384 (P-384)/`)

   - Curve: P-384 (secp384r1)
   - Key Type: EC (Elliptic Curve)
   - Use case: Higher security ECDSA signatures

5. **ES512** (`ES512 (P-521)/`)

   - Curve: P-521 (secp521r1)
   - Key Type: EC (Elliptic Curve)
   - Use case: Highest security ECDSA signatures

6. **RS256** (`RS256 (RSA)/`)
   - Algorithm: RSA
   - Key Type: RSA
   - Use case: Traditional RSA signatures

## Usage

### Resolving a DID

To resolve a DID document, convert the DID to a URL:

```javascript
// DID: did:web:truganic.github.io:did-documents:clients:farmer-client
// URL: https://truganic.github.io/did-documents/clients/farmer-client/did.json
```

### Using DIDs in Applications

1. **Resolve the DID document** from the web location
2. **Extract verification methods** from the document
3. **Use the public keys** for signature verification
4. **Verify authentication** using the methods specified in the `authentication` array

### Example: Resolving a DID Document

```javascript
async function resolveDID(did) {
  // Convert DID to URL
  const url =
    did.replace("did:web:", "https://").replace(/:/g, "/") + "/did.json";

  // Fetch the DID document
  const response = await fetch(url);
  const didDocument = await response.json();

  return didDocument;
}

// Usage
const did = "did:web:truganic.github.io:did-documents:clients:farmer-client";
const document = await resolveDID(did);
console.log(document.verificationMethod);
```

## Configuration

### Setting Up a New DID

1. **Choose a location**: Decide whether it's a client or server DID
2. **Create directory**: Create a new directory under `clients/` or `servers/`
3. **Copy template**: Use an appropriate template from `templates/` as a starting point
4. **Update DID identifier**: Modify the `id` field to match your entity name
5. **Generate keys**: Generate cryptographic keys using your chosen algorithm
6. **Update public keys**: Replace placeholder values with your actual public keys

### Generating Keys

For different algorithms:

**Ed25519:**

```bash
# Using OpenSSL or similar tools
openssl genpkey -algorithm Ed25519 -out private.pem
```

**secp256k1 (ES256K):**

```bash
openssl ecparam -genkey -name secp256k1 -out private.pem
```

**P-256 (ES256):**

```bash
openssl ecparam -genkey -name prime256v1 -out private.pem
```

### Updating Public Keys

After generating keys, extract the public key in JWK format and update the `publicKeyJwk` field in the DID document. Replace placeholder values like:

- `REPLACE_WITH_YOUR_PUBLIC_KEY_X`
- `REPLACE_WITH_YOUR_PUBLIC_KEY_Y`
- `VERY_LONG_MODULUS_BASE64URL_2048_BITS_OR_MORE`

## Deployment

### GitHub Pages Deployment

This repository is designed to be deployed via GitHub Pages:

1. **Enable GitHub Pages** in repository settings
2. **Set source** to the main branch (or docs folder if using `/docs`)
3. **Access DIDs** via `https://truganic.github.io/did-documents/{path}/did.json`

### Custom Domain Deployment

To use a custom domain:

1. **Update DID identifiers** to use your domain
2. **Deploy files** to your web server
3. **Ensure HTTPS** is enabled (required for `did:web`)
4. **Set proper CORS headers** if needed

### File Structure Requirements

For `did:web` to work correctly:

- DID documents must be accessible via HTTPS
- Files should be served with `Content-Type: application/json`
- Directory structure must match the DID path structure

## Security Considerations

### Key Management

- **Private keys** should NEVER be committed to this repository
- Store private keys securely using hardware security modules (HSM) or secure key management services
- Rotate keys periodically and update DID documents accordingly

### DID Document Integrity

- **Verify signatures** when resolving DID documents
- **Use HTTPS** to prevent man-in-the-middle attacks
- **Implement caching** with proper validation
- **Monitor for unauthorized changes** to DID documents

### Best Practices

1. **Use strong cryptographic algorithms** (prefer Ed25519 or ES256K for most use cases)
2. **Implement key rotation** procedures
3. **Monitor DID document access** and changes
4. **Use Content Security Policy** headers when serving DID documents
5. **Implement rate limiting** to prevent abuse

## Contributing

When contributing to this repository:

1. **Follow the existing structure** and naming conventions
2. **Use appropriate cryptographic algorithms** for the use case
3. **Never commit private keys** or sensitive information
4. **Update this README** if adding new sections or features
5. **Test DID resolution** before submitting changes

### Adding New DIDs

1. Create a new directory following the naming convention
2. Copy an appropriate template
3. Update the DID identifier
4. Generate and add public keys
5. Test the DID resolution
6. Submit a pull request

## References

- [W3C DID Core Specification](https://www.w3.org/TR/did-core/)
- [DID:Web Method Specification](https://w3c-ccg.github.io/did-method-web/)
- [JSON Web Key (JWK) Specification](https://tools.ietf.org/html/rfc7517)
- [JSON Web Signature (JWS) Specification](https://tools.ietf.org/html/rfc7515)

## License

[Specify your license here]

## Contact

For questions or issues related to TruGanic DID documents, please [create an issue](https://github.com/truganic/did-documents/issues) or contact the TruGanic development team.
