# **CantonID Vault — One KYC for the Entire Canton Ecosystem**

Users verify **once**. Every Canton-connected application consumes **private, reusable attestations**.  
No repeated KYC. No document uploads. Minimal cost. Full privacy.

---

## **Why It Matters**

Canton is onboarding banks, brokers, RWA platforms, custodians, and institutional venues.  
Each of them must run KYC/AML — and today they all rebuild the flow independently.  
This is slow, expensive, and destroys conversion.

---

## **Before → After**

| **Before**                    | **→** | **After (Vault)**                 |
|-------------------------------|-------|------------------------------------|
| 4 KYC processes per user      | →     | 1 verification for all apps        |
| $20–50 onboarding cost        | →     | ~$0 for verified users             |
| 30% drop-off per app          | →     | <5% drop-off                       |
| Documents stored in 4 places  | →     | Stored once (issuer)               |
| 4 AML checks                  | →     | 0 downstream AML checks            |

Vault transforms fragmented onboarding into a shared, private compliance layer.

---

## **Regulated Issuer Model**

Reusable KYC only works if trust is formalized.  
Vault introduces:

- **Vault Issuers** — licensed KYC/AML providers  
- **Reliance agreements** — apps legally rely on issuer verification  
- **Issuer liability** — issuer owns KYC/AML responsibility  
- **Shared attestations** — apps reuse verified claims, not documents  

This solves the regulatory blocker and makes cross-app KYC legally valid.

---

## **What CantonID Vault Provides**

### **Identity Contract**
- private, non-transferable identity  
- stable `identityId`  
- active/suspended status  
- selective disclosure via observers  

### **Attestation Contract**
- issued by licensed Vault Issuers  
- standardized `claimType` (`KYC_VERIFIED`, `AML_CLEAR`, `ACCREDITED_INVESTOR`)  
- validity window + revocation  
- hashes of off-ledger documents only  
- apps verify claims, never documents  

### **Dynamic AML**
Issuer performs continuous screening (sanctions, PEP, adverse media).  
Apps always see up-to-date AML status without running AML themselves.

---

## **Why This Works Only on Canton**

Canton provides:  
- contract-level privacy  
- selective disclosure  
- private cross-application interoperability  
- trusted regulated-issuer model  

This enables a **shared, reusable, private compliance layer** — something public chains cannot do.

---

## **User Flow**

1. User creates an on-ledger Identity  
2. Vault Issuer performs KYC/AML and issues attestations  
3. App is added as an observer  
4. App checks claim types, validity window, and revocation status  

**Result:** One verification → instant access across the ecosystem.

---

## **Why Builders Benefit**

Teams no longer integrate KYC vendors or manage documents.  
They only check:

> “Does this user have the required valid attestations?”

This cuts onboarding work by **~80%** and reduces costs by **5–10×**.

---

## **Use Cases**

- RWA onboarding  
- institutional lending  
- digital securities issuance  
- custody & brokerage  
- corporate onboarding  
- permissioned DEX / derivatives  

---

## **Prototype**

Figma: *(link here)*

---

**One KYC. One identity. Full ecosystem access.**
