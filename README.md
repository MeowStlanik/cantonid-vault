# CantonID Vault – Privacy-Preserving Compliance Layer for Canton

CantonID Vault provides one-time KYC and reusable, private attestations for Canton applications.  
Apps never store documents or run KYC repeatedly – they only verify claim types through Canton’s privacy model.

---

## Why

Regulated workflows (RWA, lending, OTC, custody) require KYC, AML, accreditation, revocation and strict privacy.  
Today each Canton application reimplements this separately, causing duplicated onboarding, inconsistent compliance and increased data risk.

---

## What It Provides

Identity Contract:
- private, non-transferable on-ledger identity
- stable identityId
- active/suspended status
- visibility controlled via observers

Attestation Contract:
- issued by trusted entities (banks, brokers, KYC providers)
- standardized claimType (KYC_VERIFIED, AML_CLEAR, ACCREDITED_INVESTOR, etc.)
- validity window + revocation flag
- hash of off-ledger documents
- issuer → subject binding

Applications only check claims + validity. No documents are stored.

---

## Why This Is Only Possible on Canton

Public blockchains cannot support private KYC flows because all contract state is globally visible.  
Any attestation or identity stored on a public chain immediately becomes public information.

Traditional permissioned blockchains also fall short: every application runs in isolation, so KYC must be re-implemented per app.  
There is no shared trust layer, no selective visibility, and no safe way to reuse attestations between applications.

Canton is the first platform that provides all core ingredients required for a reusable compliance layer:

- contract-level privacy (identity and attestations are visible only to authorized parties)
- selective disclosure via observers (apps see only the minimum data they are entitled to)
- strong participant identities (issuers can be trusted as regulated entities)
- secure cross-application interoperability (attestations can be consumed across apps safely)

This combination enables something that neither public chains nor traditional permissioned chains can deliver:  
a **shared, private, reusable KYC/AML foundation** for an entire ecosystem of regulated financial applications.

---

## User Flow

1. User creates Identity  
2. Regulated issuer adds Attestation  
3. App is added as observer  
4. App verifies:
   - required claim types  
   - active and non-revoked  
   - valid timestamps  

User accesses RWA, lending, custody and OTC without repeating KYC.

---

## Use Cases

- RWA onboarding  
- Institutional lending  
- OTC settlement  
- Custody & brokerage  
- Corporate onboarding  
- Permissioned DEX/derivatives  

---

## Files

daml/Identity.daml  
daml/Attestation.daml  
mockups/ 
README.md  

---

## Prototype (Figma)

https://www.figma.com/proto/N2oaCqAgvBuXi0iknHOB5l/Untitled?node-id=1-2

---

## Future Work

- JSON API  
- Next.js frontend  
- standardized claim library  
- event-driven revocation  
- identity aliases
