# CantonID Vault — One KYC for the Entire Canton Ecosystem

Users verify **once**. Every Canton-connected application consumes **private, reusable attestations**.  
No repeated KYC. No document uploads. Minimal cost. Full privacy.

---

## Why It Matters

Canton is onboarding banks, brokers, RWA platforms, custodians, stablecoin issuers, and institutional venues.  
All of them require KYC/AML — and today each application rebuilds these flows independently.

### Before
- every app integrates its own KYC provider  
- $2.5–20 per user for basic checks  
- $50+ for corporate onboarding  
- repeated onboarding → 20–40% user drop-off  
- documents handled and stored multiple times  
- fragmented identity silos

### After (with CantonID Vault)
- user verifies **once**  
- apps pay almost nothing for verified users  
- no documents handled by downstream apps  
- instant onboarding across the ecosystem  
- privacy preserved by design  
- standardized claims + revocation logic

CantonID Vault turns fragmented compliance into a shared, privacy-preserving layer.

---

## What CantonID Vault Provides

### Identity Contract
- private, non-transferable identity  
- stable `identityId`  
- active/suspended status  
- selective visibility via observers  

### Attestation Contract
- issued by regulated entities (banks, brokers, licensed KYC providers)  
- standardized `claimType` (e.g., `KYC_VERIFIED`, `AML_CLEAR`, `ACCREDITED_INVESTOR`)  
- validity window + explicit revocation  
- hashes of off-ledger documents only  
- applications verify claims, never documents  

---

## Why This Works Only on Canton

Public chains → everything is exposed.  
Typical permissioned chains → everything is siloed.

Canton enables:
- contract-level privacy  
- selective disclosure via observers  
- a trusted regulated-issuer model  
- private cross-application interoperability  

This makes a **shared, reusable, private compliance layer** possible.

---

## User Flow

1. User creates an on-ledger Identity  
2. A regulated issuer attaches an Attestation  
3. An application is added as an observer  
4. The application checks claim types, validity window, and revocation status  

**Result:** One verification → access to the entire ecosystem.

---

## Example

Alice completes KYC with a regulated issuer.  
She can instantly use:

- tokenized real estate  
- lending/borrowing platforms  
- OTC venues  
- custody & brokerage  

All auto-approved. Zero repeated onboarding.

---

## Why Builders Benefit

Teams no longer integrate KYC providers, manage documents, or maintain AML logic.  
They simply check:

> “Does this user have the required valid attestations?”

This cuts onboarding work by **~80%** and reduces operating cost by **5–10×**.

---

## Use Cases

- RWA onboarding  
- institutional lending  
- digital securities issuance  
- custody & brokerage  
- corporate onboarding  
- permissioned DEX / derivatives  

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
- claim-type registry  
- event-based revocation  
- identity aliases

---

**One KYC. One identity. Full ecosystem access.**
