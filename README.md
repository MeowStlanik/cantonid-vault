# CantonID Vault — Privacy-Preserving, Reusable Compliance for Canton

CantonID Vault is a shared KYC/AML layer for the Canton Network.  
Users complete verification **once**, and all Canton applications consume **private, reusable attestations** — no documents stored, no repeated onboarding, full privacy.

---

## Why It Matters

Regulated Canton apps require:
- KYC / AML
- Investor accreditation
- Revocation & monitoring
- Strong privacy guarantees

Today, every application rebuilds these flows in isolation, causing:
- repeated KYC per app  
- duplicated provider fees  
- fragmented identity silos  
- higher operational & regulatory risk  

CantonID Vault eliminates these issues by turning compliance into a shared, privacy-preserving service.

---

## What It Provides

### Identity Contract
- Private, non-transferable on-ledger identity  
- Stable `identityId`  
- Active/suspended status  
- Selective visibility via observers  

### Attestation Contract
- Issued by regulated entities (banks, brokers, KYC providers)  
- Standardized `claimType` (e.g., `KYC_VERIFIED`, `AML_CLEAR`, `ACCREDITED_INVESTOR`)  
- Validity window + explicit revocation  
- Hash of off-ledger documents (never stored on-chain)  
- Strong issuer → subject binding  
- Applications check claims only — never documents  

---

## Why This Works Only on Canton

Public blockchains:
- All state is public  
- Any attestation is immediately exposed  

Typical permissioned chains:
- Applications run as isolated silos  
- No shared trust or selective disclosure  
- No safe attestation reuse  

Canton provides:
- Contract-level privacy  
- Observer-based selective disclosure  
- Regulated-entity trust model  
- Secure cross-application interoperability  

Result: a **private, reusable identity layer** shared across the ecosystem.

---

## Example User Flow

1. User creates an Identity  
2. Regulated issuer adds an Attestation  
3. Application is added as an observer  
4. Application validates:
   - required claim types  
   - validity window  
   - non-revoked status  

**One KYC → ecosystem-wide access.**

Without CantonID Vault: 3 apps → 3 KYC pipelines  
With CantonID Vault: 1 KYC → instant access everywhere

---

## Example: Alice in the Canton Ecosystem

Alice completes KYC once with **RegulatedBank**.

- Tokenized real estate → auto-approved  
- Lending/borrowing → auto-approved  
- OTC trading → auto-approved  

No re-onboarding. No re-uploading documents. Full privacy.

---

## Use Cases

- RWA onboarding  
- Institutional lending  
- OTC settlement  
- Custody and brokerage  
- Corporate onboarding  
- Permissioned DEX / derivatives  

---

## Files

- `daml/Identity.daml`  
- `daml/Attestation.daml`  
- `mockups/`  
- `README.md`

---

## Prototype

Figma: https://www.figma.com/proto/N2oaCqAgvBuXi0iknHOB5l/Untitled?node-id=1-2

---

## Future Work

- JSON API  
- Next.js frontend  
- Standard claim-type registry  
- Event-driven revocation  
- Identity aliases
