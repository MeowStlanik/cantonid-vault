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
| 25–40% drop-off per app       | →     | expected <5% drop-off              |
| Documents stored in 4 places  | →     | Stored once (issuer)               |
| 4 AML checks                  | →     | 0 downstream AML checks            |

Vault transforms fragmented onboarding into a shared, private compliance layer.

---

## **Regulated Issuer Model**

Reusable KYC only works if trust is anchored in regulated entities.  
Vault introduces a simple model:

- **Vault Issuers** — licensed KYC/AML providers  
- **Reliance framework** — apps rely on issuer verification instead of running their own  
- **Issuer responsibility** — issuer maintains KYC/AML standards and monitoring  
- **Shared attestations** — apps reuse verified claims, never documents  

This removes duplicated checks and makes cross-app KYC both private and compliant.

---

## **What Vault Provides**

- private, non-transferable on-ledger identity (`identityId`)  
- standardized attestations from licensed issuers (`KYC_VERIFIED`, `AML_CLEAR`, `ACCREDITED_INVESTOR`)  
- validity window + revocation  
- apps verify claims (never documents)  
- continuous AML monitoring by the issuer, automatically reflected in attestations  

---

## **Why This Works Only on Canton**

Canton provides:  
- contract-level privacy  
- selective disclosure  
- private cross-application interoperability  
- trusted regulated-issuer model
- synchronized state for consistent issuance and revocation

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

- RWA onboarding (Black Manta, Zeconomy)
- institutional lending (Crypto Finance AG, Taurus)
- digital securities issuance (Texture Capital, D2X)
- custody & brokerage (Zodia Custody, BitGo)
- corporate onboarding (Republic, Meria)
- permissioned DEX / derivatives (Temple Digital Group, Hydra X)

These institutions already operate under strict KYC/AML requirements today.

---

## **Prototype**

Figma: https://www.figma.com/proto/N2oaCqAgvBuXi0iknHOB5l/Untitled?node-id=1-2&p=f&t=WHMoLB9evIVxoQDK-1&scaling=min-zoom&content-scaling=fixed&page-id=0%3A1
---

**One KYC. One identity. Full ecosystem access.**
