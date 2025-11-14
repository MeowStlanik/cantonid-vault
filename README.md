# CantonID Vault – Privacy Preserving Identity and Compliance Layer for the Canton Network

CantonID Vault is a simple and practical privacy preserving identity and compliance layer for the Canton Network.  
It introduces two core primitives: **private on-ledger identities** and **verifiable KYC/AML/accreditation attestations** that any regulated finance application can reuse.

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

There is no reusable, privacy preserving compliance layer that different Canton applications can share.

---

## 2. Solution – CantonID Vault

CantonID Vault adds a minimal and reusable compliance foundation:

### **Identity Contract**
A non-transferable on-ledger identity for a user or organization with:

- stable `identityId`
- lifecycle status
- controlled observers

### **Attestation Contract**
Issued by regulated entities (banks, KYC/AML providers). Includes:

- standardized `ClaimType` (KYC_VERIFIED, AML_CLEAR, ACCREDITED_INVESTOR, RWA_ELIGIBLE)
- validity window
- revocation flag
- hash of off-ledger documents  
- link to on-ledger identity via `ContractId Identity`

### **Private Visibility Through Observers**
Identities and attestations are visible only to:

- issuer  
- subject  
- authorized applications explicitly added as observers  

### **Easy Integration**
Any Canton application can check the existence and validity of required claims without accessing private documents or raw identity data.

---

## 3. Architecture

### **Identity.daml**
Fields:

- `owner : Party`
- `identityId : Text`
- `name : Text`
- `status : Status` (Active or Suspended)
- `extraObservers : [Party]`

Key choices:

- `AddObserver`
- `Deactivate`
- `Reactivate`

---

### **Attestation.daml**
Fields:

- `issuer : Party`
- `subject : Party`
- `identityCid : ContractId Identity.Identity`
- `claimType : ClaimType`
- `dataHash : Text`
- `validFrom`, `validUntil : Time`
- `revoked : Bool`

Key choices:

- `Revoke`
- `ExtendValidity`

Helper:

- `isActive : Attestation -> Time -> Bool`

---

## 4. How It Works (User Flow)

1. User creates an `Identity` contract (status = Active).  
2. A bank/KYC provider issues an `Attestation` linked via `identityCid`.  
3. Attestation is private: issuer + subject + authorized observers.  
4. Applications check:  
   - required claim types  
   - active and non-revoked  
   - valid time window  
5. If checks pass, the user can access RWA, lending, OTC and other regulated workflows **without exposing private data**.

---

## 5. Prototype Demo

Interactive Figma prototype:  
https://www.figma.com/proto/N2oaCqAgvBuXi0iknHOB5l/Untitled?node-id=1-2

Screens:

- Create Identity  
- Issue Attestation  
- Identity Vault (active + expired)

Static mockups are available in `/mockups`.

---

## 6. How To Review And Test (For Judges)

### 1. Walk through the Figma prototype:
- Create Identity  
- Issue Attestation  
- View Attestation Vault  

### 2. Review the Daml templates:
- `daml/Identity.daml`
- `daml/Attestation.daml`

Check for:

- non-transferable identity  
- issuer-controlled attestations  
- expiry and revocation  
- privacy via observers  

### 3. Integration reasoning:
Consider how the layer plugs into:

- RWA issuance  
- institutional lending  
- OTC settlement  
- permissioned trading venues  

Prototype focuses on design clarity, not a full backend.

---

## 7. Use Cases

- Tokenized RWA  
- Institutional lending  
- OTC trading  
- Permissioned DEX/perps  
- Custody, brokers, funds  
- Corporate onboarding  

CantonID Vault provides a shared compliance layer for regulated workflows.

---

## 8. Repository Structure

- `daml/Identity.daml` – identity template  
- `daml/Attestation.daml` – attestation template  
- `mockups/` – UI mockups  
- `prototype/` – placeholder for future frontend  
- `README.md` – project documentation  

---

## 9. Future Work

- Full Daml implementation + Canton DevNet deployment  
- JSON API endpoints  
- Web frontend (Next.js)  
- Larger claim library  
- Event-based revocation  
- Human-readable identity aliases  
