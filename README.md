CantonID Vault – A Unified, Privacy Preserving Identity and Compliance Layer for the Canton Network

CantonID Vault is a shared identity and compliance layer for the Canton Network. It enables one-time KYC and reusable attestations that any regulated Canton application can rely on without exposing user data. The system provides private on-ledger identities and standardized compliance attestations issued by trusted entities.

1. Problem
Regulated financial workflows such as RWA issuance, institutional lending, OTC settlement and custody require:
- verified identity
- KYC and AML screening
- accreditation checks
- revocation and expiry
- strict privacy controls

Public blockchains leak identity-related data, making them unusable for institutional-level compliance.

Canton provides identity primitives only for system participants, not for real users or organizations. This forces every application to reinvent KYC from scratch:
- separate identity storage
- separate attestation logic
- separate KYC provider integrations
- separate onboarding flows
- application-specific compliance rules

This leads to:
- fragmentation: identical logic duplicated across apps
- poor user experience: users must redo KYC repeatedly
- inconsistent compliance enforcement
- larger attack surface due to multiple independent KYC stores
- unnecessary risk from off-ledger copies of sensitive documents

There is currently no shared, private and reusable KYC and AML layer that multiple Canton applications can trust.

2. Solution – CantonID Vault
CantonID Vault introduces a minimal, standardized compliance layer based on two core templates:

Identity Contract  
A non-transferable private identity representing a user or organization with:
- stable identityId
- lifecycle status (active or suspended)
- controlled access via observers
- optional metadata

Attestation Contract  
Issued by regulated entities (banks, brokers, KYC providers). Contains:
- claimType (KYC_VERIFIED, AML_CLEAR, ACCREDITED_INVESTOR, RWA_ELIGIBLE)
- validity window
- revocation status
- hash of off-ledger documents
- issuer and subject binding

Applications no longer store KYC data or documents. They only check claim types and time-valid attestations through a private on-ledger interface.

3. Core Motivation
Today every Canton application runs its own isolated KYC workflow:
- separate onboarding
- duplicated verification logic
- multiple integrations with external KYC providers
- separate data storage and revocation handling

This creates inconsistent compliance, duplicated infrastructure, operational overhead and a poor user experience.

More importantly, it increases systemic risk:
- multiple KYC stores increase the chance of data breaches
- off-ledger document copies create uncontrolled retention
- uncoordinated revocation means outdated KYC may remain valid in some apps
- each app tends to request more data than strictly necessary

CantonID Vault removes these risks by centralizing sensitive compliance logic in one privacy-preserving on-ledger layer. Users complete KYC once, and any regulated Canton application can reuse the resulting attestations.

Why This Has Not Existed Before  
Public blockchains cannot support private KYC because all state is visible.  
Traditional permissioned chains typically implemented KYC per application, not ecosystem-wide.  

Canton is the first environment that combines:
- fine-grained contract-level privacy
- selective disclosure via observers
- trusted party identities
- safe cross-application interoperability

This makes a reusable KYC and AML foundation possible for the first time.

4. Privacy Model
Identity and Attestation contracts use strict observer-based visibility:
- issuers see their issued attestations
- subjects see their own identities and attestations
- applications see only those identities or attestations they are explicitly added to as observers

There is no global broadcast and no leakage of who has which compliance attributes. Applications receive only the minimum data necessary to verify eligibility.

5. Architecture

Identity.daml  
Fields:
- owner : Party
- identityId : Text
- name : Text
- status : Status
- extraObservers : [Party]

Choices:
- AddObserver
- Deactivate
- Reactivate

Attestation.daml  
Fields:
- issuer : Party
- subject : Party
- identityCid : ContractId Identity.Identity
- claimType : ClaimType
- dataHash : Text
- validFrom, validUntil : Time
- revoked : Bool

Choices:
- Revoke
- ExtendValidity

Helper:
- isActive : Attestation -> Time -> Bool

6. How It Works (User Flow)
1. A user creates an Identity contract.
2. A regulated entity (bank, broker or KYC provider) issues an Attestation linked to this identity.
3. The attestation remains private to the issuer, subject and any approved observer applications.
4. Applications validate:
   - required claim types
   - active and non-revoked status
   - time validity
5. If checks pass, the user can access RWA, lending, custody or OTC workflows without repeating KYC or exposing documents.

Example  
A bank issues KYC_VERIFIED.  
A broker adds AML_CLEAR.  
A custodian requires ACCREDITED_INVESTOR.  

All apps simply check attestations. None store documents. None rerun KYC. No compliance data leaks across parties.

7. Use Cases
- Tokenized real-world assets
- Institutional lending platforms
- OTC settlement workflows
- Permissioned DEX and derivatives
- Custody and brokerage operations
- Corporate onboarding

CantonID Vault functions as a shared, privacy-preserving compliance layer across the entire Canton ecosystem.

8. How to Review
1. Walk through the Figma prototype.
2. Review Identity and Attestation templates.
3. Verify:
   - non-transferable identity model
   - issuer-controlled attestation logic
   - validity and revocation mechanics
   - privacy enforcement through observers
4. Consider how applications integrate with the compliance layer.

9. Repository Structure
- daml/Identity.daml
- daml/Attestation.daml
- mockups/
- prototype/
- README.md

10. Prototype
Interactive Figma:  
https://www.figma.com/proto/N2oaCqAgvBuXi0iknHOB5l/Untitled?node-id=1-2  
Screens:
- Create Identity
- Issue Attestation
- Identity Vault

11. Future Work
- Full Daml implementation and DevNet deployment
- JSON API endpoints
- Web frontend (Next.js)
- Standardized claim library
- Event-driven revocation
- Human-readable identity aliases
