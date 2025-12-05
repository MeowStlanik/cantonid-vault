# Testing Instructions – CantonID Vault

This guide shows how to run the prototype locally, create identities, and issue attestations.

---

## 1. Requirements

- Daml SDK 2.x installed  
- Canton Community environment or `daml start`  
- Git installed  

---

## 2. Run the Ledger

### Option A: Run with Daml Sandbox

```bash
daml start
```

This launches:
- Sandbox ledger  
- HTTP JSON API on port 7575  
- Navigator interface  

---

## 3. Compile the Daml contracts

```bash
daml build
```

---

## 4. Deploy to Sandbox

```bash
daml start
```

Templates available:
- `Identity.Identity`  
- `Attestation.Attestation`  
- `AccessControl.AccessGrant`  

---

## 5. Create a Test Identity

### Using Navigator

1. Open Navigator  
2. Select party **Alice**  
3. Create contract **Identity**  
4. Fields:  
   - name: "Alice Example"  
   - identityId: "alice-001"  

### Using JSON API

```json
POST http://localhost:7575/v1/create
{
  "templateId": "Identity:Identity",
  "payload": {
    "owner": "Alice",
    "name": "Alice Example",
    "identityId": "alice-001"
  }
}
```

---

## 6. Issue a KYC Attestation

Issuer: **BankNode**

```json
POST http://localhost:7575/v1/create
{
  "templateId": "Attestation:Attestation",
  "payload": {
    "issuer": "BankNode",
    "subject": "Alice",
    "identityId": "alice-001",
    "claimType": "KYC_VERIFIED",
    "validUntil": "2026-12-31",
    "active": true
  }
}
```

---

## 7. Application Requests Access

```json
POST http://localhost:7575/v1/create
{
  "templateId": "AccessControl:AccessRequest",
  "payload": {
    "requester": "App1",
    "identityOwner": "Alice",
    "identityId": "alice-001"
  }
}
```

Alice approves:

- Open the AccessRequest  
- Exercise **GrantAccess**  

---

## 8. Verify Attestations as App1

```json
POST http://localhost:7575/v1/query
{
  "templateIds": ["Attestation:Attestation"]
}
```

App1 only sees attestations it is authorized to view.

---

## 9. Expected Outcome

- Identity created  
- Attestations issued  
- Third party requests access  
- Owner grants access  
- App verifies compliance  
- Private user data stays fully confidential  
