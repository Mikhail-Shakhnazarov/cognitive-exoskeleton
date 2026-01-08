# Changelog

Append-only journal of state transitions. Each entry documents what changed, why, verification status, and remaining issues.

---

## [2025-01-06T14:30] src/auth/registration.js

**Artifact:** code  
**Spec:** SPEC-001#AUTH-001, AUTH-005

- **Added:** User registration endpoint with email validation and password hashing
- **Added:** Email format validation using RFC 5322 simplified regex
- **Added:** bcrypt password hashing with cost factor 12
- **Added:** Unique email constraint check before insert

### Verification
✅ Registration with valid email/password succeeds  
✅ Password stored hashed (not plaintext) in database  
✅ Malformed email rejected with 400  
✅ Duplicate email rejected with 409

### Friction
- FR-001 remains open (uniqueness race condition - using DB constraint for now)

---

## [2025-01-06T16:45] src/auth/login.js

**Artifact:** code  
**Spec:** SPEC-001#AUTH-002, AUTH-003

- **Added:** Login endpoint with password verification
- **Added:** Session token generation (crypto.randomBytes)
- **Added:** Rate limiting middleware (5 attempts per IP per 15min)
- **Changed:** Session tokens now stored hashed in database

### Verification
✅ Login with correct credentials returns token  
✅ Login with wrong password returns 401  
✅ 6th login attempt within 15min returns 429  
⏳ Session token validation (pending next session)

### Friction
- FR-002 created (rate limiting scope - per-IP vs per-email)
- Rate limiting currently per-IP only pending decision

---

## [2025-01-06T18:00] Decision: Session storage strategy

**Artifact:** decision  
**Spec:** SPEC-001 (architecture)

- **Decided:** Redis primary + PostgreSQL persistence for sessions
- **Added:** ADR-003 documenting choice and rationale
- **Resolved:** FR-000 (session storage)

### Verification
N/A (architecture decision)

### Friction
None

---

## [2025-01-05T10:00] SPEC-001 created

**Artifact:** spec  
**Spec:** SPEC-001

- **Added:** Complete authentication module specification
- **Added:** Requirements (5 MUST, 2 SHOULD, 1 MAY)
- **Added:** Interface definitions and constraints
- **Open:** 2 items marked for operator decision

### Verification
Spec reviewed by operator, marked ACTIVE

### Friction
- FR-001 created from OPEN-001
- FR-002 created from OPEN-002

---

## [2025-01-04T15:30] Project initialization

**Artifact:** infrastructure  
**Spec:** N/A (setup)

- **Added:** Repository structure
- **Added:** PostgreSQL schema (users, sessions tables)
- **Added:** Basic Express.js server setup
- **Added:** Development environment configuration

### Verification
✅ Server starts successfully  
✅ Database connection established  
✅ Migrations run cleanly

### Friction
None

---

## Format Notes

Each entry must include:
- Timestamp (ISO 8601 format)
- Artifact type (code | config | doc | decision)
- Spec reference (which requirement being satisfied)
- Changes (Added/Changed/Fixed/Removed)
- Verification status (✅ passed, ❌ failed, ⏳ pending, N/A)
- Friction (new, resolved, remaining)

Changes without verification are incomplete.
