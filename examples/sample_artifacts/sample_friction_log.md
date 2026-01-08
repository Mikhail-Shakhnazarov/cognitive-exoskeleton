# Friction Log

Typed blocked states requiring operator decision.

---

## Active Friction

### FR-001 | Email Uniqueness Race Condition
**Type:** Feasibility  
**Spec:** SPEC-001#OPEN-001  
**Context:** User registration flow  

**Issue:** If two registration requests with same email arrive simultaneously, both might pass uniqueness check before either commits to database.

**Options:**
1. Database unique constraint only (let DB handle, catch exception, retry)
2. Application-level distributed lock (Redis/similar before DB insert)
3. Optimistic locking with version field
4. Accept race as rare edge case, rely on DB constraint

**Impact:** 
- Option 1: Simpler but requires retry logic in registration handler
- Option 2: More complex, requires additional infrastructure
- Option 3: Cleanest but requires migration to add version field
- Option 4: Acceptable if registration volume is low

**Proposed Resolution:** Option 1 - DB constraint + catch + appropriate error response

**Status:** OPEN  
**Created:** 2025-01-06  
**Assigned:** Operator

---

### FR-002 | Rate Limiting Scope
**Type:** Semantic  
**Spec:** SPEC-001#OPEN-002  
**Context:** Login rate limiting

**Issue:** AUTH-003 specifies "per IP" but doesn't address:
- Should we also limit per-email (prevent dictionary attack on single account)
- Should we limit per IP+email combination
- What about legitimate users behind shared IP (office, VPN)

**Options:**
1. Per-IP only (current spec)
2. Per-email only (different attack vector)
3. Both (conservative)
4. Per-IP + elevated limit per-email (balanced)

**Impact:**
- Option 1: Simple but vulnerable to targeted account attacks
- Option 2: Doesn't prevent distributed attacks
- Option 3: Most secure but may cause false positives
- Option 4: Complex but handles both attack vectors

**Proposed Resolution:** Option 4 - 5 attempts per IP per 15min + 10 attempts per email per hour

**Status:** OPEN  
**Created:** 2025-01-06  
**Assigned:** Operator

---

## Resolved Friction

### FR-000 | Session Storage Strategy
**Type:** Architecture  
**Spec:** SPEC-001 (general)  
**Context:** Where to store session tokens

**Issue:** Sessions could be stored in: database (PostgreSQL), cache (Redis), or both.

**Options:**
1. Database only - simple, persistent, slower
2. Redis only - fast, but loss on restart
3. Both - fast read, persistent, complex

**Resolution:** Option 3 - Redis primary with DB persistence  
**Rationale:** Balances performance and reliability. Write to both; read from Redis; fall back to DB if Redis miss.  
**Documented:** ADR-003  
**Decided By:** Operator  
**Closed:** 2025-01-05

---

### FR-003 | Password Strength Validation
**Type:** Scope  
**Spec:** SPEC-001#constraints  
**Context:** What constitutes acceptable password

**Issue:** Spec says ">=8 characters" but should we enforce:
- Character class requirements (uppercase, lowercase, number, symbol)
- Common password blacklist
- Similarity to username/email

**Resolution:** Minimal for v1 - only length requirement  
**Rationale:** Additional validation deferred to SPEC-002 (password policy enhancement). Current scope: basic authentication only.  
**Decided By:** Operator  
**Closed:** 2025-01-06

---

## Friction Statistics

- **Total Created:** 4
- **Currently Open:** 2
- **Resolved:** 2
- **Average Resolution Time:** 1 day

---

## Notes

Friction items should be resolved before marking spec COMPLETE. OPEN items in specs automatically generate friction entries.

Update status to RESOLVED when operator makes binding decision. Include rationale and any relevant documentation links (specs, ADRs, patterns).
