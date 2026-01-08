# SPEC-001: User Authentication Module

> Status: ACTIVE  
> Created: 2025-01-05  
> Updated: 2025-01-06  
> Target: `src/auth/`

---

## Summary

Implement secure user authentication with email/password login, session management, and password reset functionality. System must support both web and API access patterns.

---

## Scope

**In:**
- Email/password registration and login
- Session token generation and validation
- Password hashing (bcrypt, cost factor 12)
- Password reset via email token
- Rate limiting on login attempts (5 per 15 minutes per IP)
- Session expiration (24 hours default, configurable)

**Out:**
- OAuth/social login (future spec)
- Multi-factor authentication (future spec)
- User profile management beyond authentication
- Email delivery infrastructure (assume service exists)

---

## Requirements

### MUST

1. **AUTH-001** -- Hash passwords using bcrypt with cost factor 12
   - Acceptance: No plaintext passwords in database; bcrypt.compare validates correctly

2. **AUTH-002** -- Generate cryptographically secure session tokens (32 bytes, hex-encoded)
   - Acceptance: Tokens generated with crypto.randomBytes; stored hashed in database

3. **AUTH-003** -- Rate limit login attempts to 5 per IP per 15 minutes
   - Acceptance: 6th attempt within window returns 429; counter resets after window

4. **AUTH-004** -- Expire sessions after 24 hours by default
   - Acceptance: Token validation checks created_at + ttl; expired tokens rejected

5. **AUTH-005** -- Validate email format before registration
   - Acceptance: Regex validation; malformed emails rejected with 400

### SHOULD

1. **AUTH-101** -- Return meaningful error codes (400/401/429) not generic 500
2. **AUTH-102** -- Log authentication events (success, failure, rate limit) for audit

### MAY

1. **AUTH-201** -- Support configurable session TTL per-user or per-request

---

## Interfaces

**Inputs:**
- POST `/auth/register` - `{ email, password }`
- POST `/auth/login` - `{ email, password }`
- POST `/auth/logout` - `{ token }`
- POST `/auth/reset-request` - `{ email }`
- POST `/auth/reset-confirm` - `{ token, newPassword }`
- GET `/auth/validate` - `Authorization: Bearer {token}`

**Outputs:**
- Success: `{ success: true, token, message }`
- Failure: `{ success: false, error, code }`

**Dependencies:**
- PostgreSQL database with users and sessions tables
- Email service API for password reset emails
- Redis or equivalent for rate limiting state

---

## Constraints

1. Passwords must be >=8 characters, <=128 characters
2. Email addresses must be unique (database constraint)
3. Session tokens must be 64 hex characters
4. Rate limiting state must survive server restarts (persistent store)
5. Password reset tokens expire after 1 hour

---

## Open

| ID | Description | Closure |
|----|-------------|---------|
| OPEN-001 | How should we handle email uniqueness race conditions | Database unique constraint + retry logic or application-level locking |
| OPEN-002 | Should failed login attempts be per-email or per-IP | Clarify anti-abuse strategy |

Port A: return friction on OPEN items, do not resolve.

---

## Notes

**Security considerations:**
- Timing attacks: Use constant-time comparison for tokens
- SQL injection: Use parameterized queries throughout
- Session fixation: Generate new token on login, invalidate on logout

**Pattern references:**
Check `patterns/BUG_PATTERNS.md`:
- JS-002 for bcrypt async handling
- GEN-002 for error logging requirements

**Related decisions:**
- ADR-003 covers session storage strategy (database vs Redis)

---

## Verification

1. **Registration flow**: Create user with valid email/password -> success response -> user exists in DB with hashed password
2. **Login flow**: Attempt login with correct credentials -> token returned -> token validates on subsequent request
3. **Failed login**: Attempt login with wrong password -> 401 returned -> login counter increments
4. **Rate limiting**: Make 6 login attempts within 15min -> 6th returns 429 -> error message indicates rate limit
5. **Session expiration**: Create session, fast-forward clock 25 hours -> token validation fails with appropriate error
6. **Password reset**: Request reset -> email sent -> use token to set new password -> can login with new password

---

## Lifecycle

| Date | Status | Note |
|------|--------|------|
| 2025-01-05 | DRAFT | Initial draft from requirements discussion |
| 2025-01-06 | ACTIVE | Operator approved; OPEN items to be resolved during implementation |
