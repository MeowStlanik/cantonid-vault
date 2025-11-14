# CantonID Vault – Privacy-Preserving Identity and Attestation Layer for the Canton Network

CantonID Vault is a prototype of a privacy-preserving identity and attestation layer built for the Canton Network using Daml concepts.  
It focuses on enabling compliant on-ledger identity, KYC/AML/accreditation attestations, and eligibility checks for regulated finance and tokenized real-world assets (RWA).

---

## 1. Problem Statement

Regulated financial workflows – such as RWA issuance, institutional lending, and OTC settlement – require reliable identity, KYC/AML proofs, accreditation status, and auditable attestations.  
Existing onchain identity systems on public chains are fully transparent and therefore unsuitable for regulated institutions.  
At the same time, Canton’s built-in identity focuses on system participants (parties, nodes, keys), not on user- or organization-level identity with verifiable compliance data.  
There is no reusable, privacy-preserving identity and attestation primitive that applications across Canton can rely on.

---

## 2. Proposed Solution – CantonID Vault

CantonID Vault introduces a minimal, reusable identity and attestation layer:

- **On-ledger Identity Contract** – a non-transferable identity contract per user or institution.
- **Verifiable Attestations** – KYC/AML/accreditation attestations issued by regulated institutions.
- **Role-Based Visibility** – only authorized parties can see or rely on attestations.
- **Standardized Claims** – common claim types like `KYC_VERIFIED`, `AML_CLEAR`, `ACCREDITED_INVESTOR`, `RWA_ELIGIBLE`.
- **Revocation and Expiry** – attestations can expire or be revoked by the issuer.
- **Composable Primitive** – any Canton application (RWA, lending, OTC, DEX, custody) can check compliance by querying attestations instead of raw private data.

The goal is to provide a **compliance-first identity layer** that matches Canton’s privacy and institutional focus.

---

## 3. Architecture Overview

Conceptually, the system consists of three main components:

1. **Identity template (Identity.daml)**  
   - Represents a user or institution on-ledger.  
   - Non-transferable, controlled by the owner party.  
   - Holds a stable `identityId` used to link attestations.

2. **Attestation template (Attestation.daml)**  
   - Issued by regulated institutions (banks, KYC/AML providers, compliance services).  
   - Contains claim type, hash of off-ledger documents, validity period, and revocation flag.  
   - Visible only to issuer, subject, and explicitly added observers.

3. **Applications using CantonID Vault**  
   - RWA issuers, lending apps, OTC desks, and permissioned DEXs query attestations for specific identities.  
   - They check for required claims (e.g. `KYC_VERIFIED`, `ACCREDITED_INVESTOR`) without accessing private user data.

This architecture fits naturally with Daml’s multi-party contracts and Canton’s privacy model.

---

## 4. Prototype Demo

The current prototype focuses on UX and flow rather than a full backend implementation.

🔗 **Figma Prototype:**  
`<PUT YOUR FIGMA LINK HERE>`

The prototype shows three main screens:

1. **Create Identity** – user/institution creates an on-ledger identity entry.  
2. **Issue Attestation** – regulated issuer attaches a KYC/AML/accreditation attestation.  
3. **Identity Attestation Vault** – view of active/inactive attestations, including expired ones.

---

## 5. How It Works (User Flow)

1. A user or institution creates an Identity contract via the “Create Identity” flow.  
2. A regulated issuer (e.g. bank, KYC provider) selects an identity and issues an Attestation (e.g. `KYC_VERIFIED`, `AML_CLEAR`, `ACCREDITED_INVESTOR`) with a validity period.  
3. The Attestation is linked to the identity via `identityId` and visible only to the relevant parties.  
4. A financial application (RWA issuer, lending protocol, OTC desk) checks if the required attestations exist and are valid (not expired, not revoked).  
5. If checks pass, the application allows the user to participate in the workflow (subscribe to RWA, open a credit line, execute OTC settlement, etc.) without ever exposing raw private identity data on-ledger.

---

## 6. Testing Instructions (for Judges)

This repository is submitted as an ideathon prototype.  
To review and “test” the idea:

1. **Prototype Walkthrough**
   - Open the Figma link from the section above.
   - Click through the flow:
     1. Create Identity
     2. Issue Attestation (choose claim type and validity)
     3. View Identity Attestation Vault (review active and inactive/expired attestations)

2. **Conceptual Daml Templates**
   - Open `daml/Identity.daml` and `daml/Attestation.daml`.
   - Review the template fields and choices that model:
     - non-transferable identity
     - issuer-controlled attestations
     - revocation and expiry
     - role-based visibility via signatories and observers

3. **Architecture Reasoning**
   - Use the README and mockup screenshots in `/mockups` to understand how CantonID Vault can plug into:
     - RWA issuance flows
     - institutional lending
     - OTC settlement
     - permissioned trading venues

The goal of this prototype is to present a realistic and implementable design, not a fully implemented production codebase.

---

## 7. Potential Impact and Use Cases

CantonID Vault can be used in:

- **Tokenized RWA Issuance** – only verified and eligible investors can subscribe.  
- **Institutional Lending** – lenders can rely on attestations instead of custom KYC integrations.  
- **OTC Desks** – counterparties are verified and compliant without leaking private details.  
- **Permissioned DEX / Perps** – enforcement of access based on attestations rather than wallet lists.  
- **Custody, Broker-Dealers, Funds** – shared, reusable compliance layer across multiple apps.  
- **Corporate Onboarding** – on-ledger, privacy-preserving corporate identity and eligibility.

This makes Canton more attractive as a base layer for regulated and institutional finance.

---

## 8. Tools, Technologies, Methods

- **Canton Network & Daml concepts** (identity, multi-party contracts, observers, privacy)
- **Daml template design** for Identity and Attestation
- **Figma** for UX/mockup prototyping
- (Future work) JSON API and Canton DevNet integration
- (Future work) Frontend (e.g. Next.js) for production-grade UI

---

## 9. Future Work

- Implement full Daml modules and integration with a Canton DevNet instance.  
- Add JSON API endpoints for identity creation and attestation issuance.  
- Build a simple frontend on top (Next.js / React).  
- Extend attestation types, add risk flags and jurisdiction-specific requirements.  
- Add an optional domain/alias layer for human-readable identity referencing.
