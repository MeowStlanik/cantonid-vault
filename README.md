# CantonID Vault - Privacy Preserving Identity and Compliance Layer for the Canton Network

CantonID Vault is a simple and practical privacy preserving identity and compliance layer for the Canton Network.  
It introduces two core primitives - private on-ledger identities and verifiable KYC/AML/accreditation attestations - that any regulated finance application can reuse.

---

## 1. Problem

Regulated financial processes like RWA issuance, institutional lending, OTC settlement and custody require:

- verified identity
- KYC/AML checks
- accreditation status
- revocation and expiry
- strict privacy

Public blockchains expose all identity data, which makes them unusable for institutional workflows.  
Canton has built in identity for system participants (nodes, parties), but not for real users or organizations.

There is no reusable, privacy preserving compliance layer that different Canton applications can share.

---

## 2. Solution - CantonID Vault

CantonID Vault adds a minimal and reusable compliance foundation:

- **Identity Contract**  
  A non transferable on-ledger identity for a user or organization, with a stable `identityId`, lifecycle status, and controlled observers.

- **Attestation Contract**  
  Issued by regulated entities (banks, KYC/AML providers).  
  Uses a standardized `ClaimType` (KYC_VERIFIED, AML_CLEAR, ACCREDITED_INVESTOR, RWA_ELIGIBLE), validity window, revocation flag and a hash of off-ledger documents.  
  Attestations link directly to the on-ledger identity via `ContractId Identity`.

- **Private Visibility Through Observers**  
  Identities and attestations are visible only to the issuer, the subject, and authorized applications that are explicitly added as observers.

- **Easy Integration**  
  Any Canton application can check the existence and validity of required claims without accessing private documents or raw identity data.

---

## 3. Architecture

### Identity.daml

The `Identity` template:

- `owner : Party` - identity owner  
- `identityId : Text` - stable identifier used in off-ledger systems  
- `name : Text` - human readable name  
- `status : Status` - `Active` or `Suspended`  
- `extraObservers : [Party]` - additional applications allowed to see the identity  

Key choices:

- `AddObserver` - owner can add an observer application  
- `Deactivate` / `Reactivate` - lifecycle management of the identity

### Attestation.daml

The `Attestation` template:

- `issuer : Party` - regulated issuer (bank, KYC provider)  
- `subject : Party` - identity owner  
- `identityCid : ContractId Identity.Identity` - link to the on-ledger identity  
- `claimType : ClaimType` - one of `KYC_VERIFIED`, `AML_CLEAR`, `ACCREDITED_INVESTOR`, `RWA_ELIGIBLE`  
- `dataHash : Text` - hash of off-ledger documents  
- `validFrom`, `validUntil : Time` - validity window  
- `revoked : Bool` - revocation flag  

Key choices:

- `Revoke` - issuer can revoke the attestation  
- `ExtendValidity` - issuer can extend the validity period  

Helper:

- `isActive : Attestation -> Time -> Bool` - checks if an attestation is currently valid and not revoked

---

## 4. How It Works (User Flow)

1. A user creates an `Identity` contract with status `Active`.  
2. A bank or KYC provider issues an `Attestation` linked to that identity via `identityCid`.  
3. The attestation is private, visible only to the subject, issuer and allowed applications.  
4. Any application checks:  
   - required claim types exist  
   - they are active (`isActive` evaluates to true)  
   - not revoked  
5. If checks pass, the user is allowed to participate in RWA, lending, OTC, or other regulated workflows without exposing any personal data.

---

## 5. Prototype Demo

Interactive Figma prototype:  
https://www.figma.com/proto/N2oaCqAgvBuXi0iknHOB5l/Untitled?node-id=1-2

Screens:

- Create Identity  
- Issue Attestation  
- Identity Vault (active plus expired)

Static mockups are also available in `/mockups`.

---

## 6. How To Review And Test (For Judges)

1. **Walk through the Figma prototype.**  
   Follow the flow:
   - Create Identity
   - Issue Attestation
   - View Identity Attestation Vault (active and expired claims)

2. **Review the conceptual Daml templates.**  
   Open:

   - `daml/Identity.daml`
   - `daml/Attestation.daml`

   and check:

   - non transferable identity
   - issuer controlled attestations
   - revocation and expiry
   - privacy via signatories and observers

3. **Reason about integration.**  
   Consider how CantonID Vault can plug into:

   - RWA issuance flows  
   - institutional lending  
   - OTC settlement  
   - permissioned trading venues

The prototype focuses on clarity and realistic design, not on a full backend implementation.

---

## 7. Use Cases

- Tokenized RWA  
- Institutional lending  
- OTC trading  
- Permissioned DEX and perps  
- Custody, brokers, funds  
- On ledger corporate onboarding

CantonID Vault makes Canton more suitable for regulated and institutional finance.

---

## 8. Repository Structure

- `daml/Identity.daml` - identity contract template  
- `daml/Attestation.daml` - attestation contract template  
- `mockups/` - UI mockups (PNG) used in the prototype  
- `prototype/` - placeholder for potential frontend or integration code  
- `README.md` - project overview and testing instructions

---

## 9. Future Work

- Full Daml implementation and deployment to a Canton DevNet instance  
- JSON API endpoints for identity creation and attestation issuance  
- Simple web frontend (Next.js or React) for production grade UI  
- Extended claim library and jurisdiction specific requirements  
- Event based revocation and audit trails  
- Human readable identity aliases and domain mapping
