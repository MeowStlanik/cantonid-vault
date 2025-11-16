# CantonID Vault – Privacy-Preserving Compliance Layer for Canton

CantonID Vault provides **one-time KYC** and **reusable, private attestations** for Canton applications.  
Apps never store documents or rerun verification – they only check claim types through Canton’s privacy model.

---

## Why

Regulated workflows (RWA, lending, OTC, custody) require:

- KYC
- AML
- Accreditation
- Revocation
- Strict privacy

Today, each Canton application reimplements these flows separately, causing:

- Duplicated onboarding
- Inconsistent compliance
- Increased data risk

---

## What It Provides

### Identity Contract

- Private, non-transferable on-ledger identity  
- Stable `identityId`  
- Active/suspended status  
- Visibility controlled via observers  

### Attestation Contract

- Issued by trusted entities (banks, brokers, KYC providers)  
- Standardized `claimType` (e.g., `KYC_VERIFIED`, `AML_CLEAR`, `ACCREDITED_INVESTOR`)  
- Validity window + revocation flag  
- Hash of off-ledger documents  
- Issuer → subject binding  
- Apps only check claims and validity – **no documents stored**

---

## Why This Is Only Possible on Canton

Public chains:
- All contract state is globally visible  
- Any attestation becomes public immediately  

Traditional permissioned chains:
- Each app runs in isolation  
- No shared trust & selective visibility  
- No safe attestation reuse  

---

Canton delivers:

- **Contract-level privacy**
- **Selective disclosure via observers**
- **Strong regulated identities**
- **Secure cross-application interoperability**

**Result:** A shared, private, reusable KYC/AML layer for regulated financial ecosystems.

---

## User Flow

1. User creates Identity  
2. Regulated issuer adds Attestation  
3. App is added as observer  
4. App verifies:
   - Required claim types  
   - Non-revoked  
   - Valid timestamps  

**User now accesses RWA, lending, custody, OTC without repeated KYC.**

---

## 📌 Example: Alice in Canton Ecosystem

Alice completes KYC once with **RegulatedBank**.

- Invests in tokenized real estate → approved instantly  
- Borrows against her tokens → approved instantly  
- Trades on OTC platform → approved instantly  

> Zero re-onboarding. Zero document uploads. Full privacy.

**Without CantonID Vault:**  
3 apps = 3 separate KYC processes = 3 data silos  

**With CantonID Vault:**  
1 KYC = ecosystem-wide access

---

## Use Cases

- RWA onboarding  
- Institutional lending  
- OTC settlement  
- Custody & brokerage  
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

[Figma Prototype](https://www.figma.com/proto/N2oaCqAgvBuXi0iknHOB5l/Untitled?node-id=1-2)

---

## Future Work

- JSON API  
- Next.js frontend  
- Standardized claim library  
- Event-driven revocation  
- Identity aliases  
