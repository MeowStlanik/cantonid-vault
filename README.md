# CantonID Vault – Privacy-Preserving Identity and Compliance Layer for the Canton Network

CantonID Vault is a simple and practical privacy-preserving identity and compliance layer for the Canton Network.  
It introduces two core primitives – private on-ledger identities and verifiable KYC/AML/accreditation attestations – that any regulated finance application can reuse.

---

## 1. Problem

Regulated financial processes like RWA issuance, institutional lending, OTC settlement and custody require:

- verified identity
- KYC/AML checks
- accreditation status
- revocation and expiry
- strict privacy

Public blockchains expose all identity data, which makes them unusable for institutional workflows.  
Canton has built-in identity for system participants (nodes, parties), but not for real users or organizations.

There is no reusable, privacy-preserving compliance layer that different Canton applications can share.

---

## 2. Solution – CantonID Vault

CantonID Vault adds a minimal and reusable compliance foundation:

- **Identity Contract**  
  A non-transferable on-ledger identity for a user or organization.

- **Attestation Contract**  
  Issued by regulated entities (banks, KYC/AML providers).  
  Includes claim type, validity period, document hash, and revocation flag.

- **Private Visibility Through Observers**  
  Attestations are visible only to the issuer, the subject, and authorized applications.

- **Standardized Claim Types**  
  KYC_VERIFIED, AML_CLEAR, ACCREDITED_INVESTOR, RWA_ELIGIBLE.

- **Easy Integration**  
  Any Canton application can check the existence and validity of required claims without accessing private documents.

---

## 3. Architecture

### Identity.daml
- owner is the user  
- non-transferable contract  
- unique `identityId`  
- supports adding allowed observers

### Attestation.daml
- issuer is a regulated entity  
- contains `claimType`, `validFrom`, `validUntil`, `revoked`  
- references `identityId`  
- visibility defined via observers

---

## 4. How It Works (User Flow)

1. A user creates an Identity contract.  
2. A bank or KYC provider issues an Attestation linked to that identityId.  
3. The attestation is private, visible only to permitted parties.  
4. Any application checks:  
   - required claims exist  
   - they are valid  
   - not revoked  
5. If checks pass, the user is allowed to participate in RWA, lending, OTC, or other regulated workflows without exposing any personal data.

---

## 5. Prototype Demo

Interactive Figma prototype:  
https://www.figma.com/proto/N2oaCqAgvBuXi0iknHOB5l/Untitled?node-id=1-2

Screens:
- Create Identity  
- Issue Attestation  
- Identity Vault (active + expired)

---

## 6. Judge Instructions

1. Walk through the Figma prototype.  
2. Review the conceptual Daml templates:
   - `daml/Identity.daml`
   - `daml/Attestation.daml`  
3. Check the core logic:
   - privacy via observers  
   - expiry  
   - revocation  
4. Evaluate how the layer integrates with:
   - RWA flows  
   - lending  
   - OTC settlement  
   - permissioned trading venues

The prototype focuses on clarity and realistic design, not full backend implementation.

---

## 7. Use Cases

- Tokenized RWA  
- Institutional lending  
- OTC trading  
- Permissioned DEX/perps  
- Custody, brokers, funds  
- On-ledger corporate onboarding

CantonID Vault makes Canton more suitable for regulated and institutional finance.

---

## 8. Future Work

- Full Daml implementation  
- JSON API endpoints  
- Simple web frontend (Next.js)  
- Extended claim library  
- Event-based revocation  
- Human-readable identity aliases
