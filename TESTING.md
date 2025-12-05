# Testing Instructions – CantonID Vault

This guide describes how to run the CantonID Vault prototype locally, create identities, issue attestations, and test access control with selective disclosure.

---

## 1. Requirements

Before running the prototype, ensure the following are installed:

- **Daml SDK 2.x**
- **Canton Community** or the built‑in Sandbox (`daml start`)
- **Git**
- Optional: **Daml Navigator** for UI-based testing

Clone the repository:

```bash
git clone <your-repo-url>
cd cantonid-vault
```

---

## 2. Build the Daml Contracts

Compile all templates:

```bash
daml build
```

This generates the `.dar` archive in `.daml/dist/`.

---

## 3. Start the Ledger (Sandbox)

Run a local Sandbox ledger with JSON API and Navigator:

```bash
daml start
```

This starts:

- Sandbox ledger  
- JSON API at **http://localhost:7575**  
- Navigator UI  

---

## 4. Available Templates

The following templates become available once the ledger is running:

- `Identity.Identity`
- `Attestation.Attestation`
- `AccessControl.AccessRequest`
- `AccessControl.AccessGrant`

These represent the full identity → attestation → access workflow.

---

## 5. Create a Test Identity

### Option A – Using Navigator

1. Open Navigator  
2. Select party **Alice**  
3. Create a contract of type **Identity**  
4. Fields:
   - `name`: "Alice Example"
   - `identityId`: "alice-001"
   - `status`: "Active"
   - `extraObservers`: []

### Option B – Using JSON API

```json
POST http://localhost:7575/v1/create?party=Alice
{
  "templateId": "Identity:Identity",
  "payload": {
    "owner": "Alice",
    "identityId": "alice-001",
    "name": "Alice Example",
    "status": "Active",
    "extraObservers": []
  }
}
```

---

## 6. Issue a KYC Attestation

Issuer: **BankNode**

```json
POST http://localhost:7575/v1/create?party=BankNode
{
  "templateId": "Attestation:Attestation",
  "payload": {
    "issuer": "BankNode",
    "subject": "Alice",
    "identityCid": "<CONTRACT_ID_IDENTITY>",
    "claimType": "KYC_VERIFIED",
    "dataHash": "sha256:placeholder",
    "validFrom": "2025-01-01T00:00:00Z",
    "validUntil": "2026-12-31T00:00:00Z",
    "revoked": false,
    "extraObservers": []
  }
}
```

---

## 7. Application Requests Access

```json
POST http://localhost:7575/v1/create?party=App1
{
  "templateId": "AccessControl:AccessRequest",
  "payload": {
    "requester": "App1",
    "identityOwner": "Alice",
    "identityId": "alice-001"
  }
}
```

Alice approves in Navigator by exercising **GrantAccess**.

---

## 8. Verify Attestations as App1

```json
POST http://localhost:7575/v1/query?party=App1
{
  "templateIds": ["Attestation:Attestation"]
}
```

App1 can request access (recorded as AccessGrant), 
but in this prototype attestations are still only visible to issuer and subject.

---

## 9. Expected Outcome

- Identity created  
- KYC attestation issued  
- App requests access  
- User grants access  
- Access grants are recorded on-ledger (AccessGrant), but this prototype does not yet wire them to attestation visibility.
- All personal data remains private  

---
