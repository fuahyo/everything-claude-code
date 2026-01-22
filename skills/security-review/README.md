# Security Review Skill

Provides comprehensive security checklist and patterns for secure code development.

## Purpose

This skill ensures all code follows security best practices:
- **Vulnerability detection** - Identifies security risks
- **Best practices enforcement** - Applies security patterns
- **Comprehensive checklist** - Covers OWASP Top 10 and more
- **Project-specific guidance** - Tailored to your stack

## When to Use

This skill activates automatically when:
- Implementing authentication or authorization
- Handling user input or file uploads
- Creating new API endpoints
- Working with secrets or credentials
- Implementing payment features
- Storing or transmitting sensitive data
- Integrating third-party APIs

## When NOT to Use

- For non-security code reviews
- Documentation updates
- Simple formatting changes

## Security Checklist

### 1. Secrets Management
- [ ] No hardcoded API keys, tokens, or passwords
- [ ] All secrets in environment variables
- [ ] `.env.local` in .gitignore
- [ ] No secrets in git history
- [ ] Production secrets in hosting platform

### 2. Input Validation
- [ ] All user inputs validated with schemas
- [ ] File uploads restricted (size, type, extension)
- [ ] No direct use of user input in queries
- [ ] Whitelist validation (not blacklist)
- [ ] Error messages don't leak sensitive info

### 3. SQL Injection Prevention
- [ ] All database queries use parameterized queries
- [ ] No string concatenation in SQL
- [ ] ORM/query builder used correctly
- [ ] Supabase queries properly sanitized

### 4. Authentication & Authorization
- [ ] Tokens stored in httpOnly cookies (not localStorage)
- [ ] Authorization checks before sensitive operations
- [ ] Row Level Security enabled in Supabase
- [ ] Role-based access control implemented
- [ ] Session management secure

### 5. XSS Prevention
- [ ] User-provided HTML sanitized
- [ ] CSP headers configured
- [ ] No unvalidated dynamic content rendering
- [ ] React's built-in XSS protection used

### 6. CSRF Protection
- [ ] CSRF tokens on state-changing operations
- [ ] SameSite=Strict on all cookies
- [ ] Double-submit cookie pattern implemented

### 7. Rate Limiting
- [ ] Rate limiting on all API endpoints
- [ ] Stricter limits on expensive operations
- [ ] IP-based rate limiting
- [ ] User-based rate limiting (authenticated)

### 8. Sensitive Data Exposure
- [ ] No passwords, tokens, or secrets in logs
- [ ] Error messages generic for users
- [ ] Detailed errors only in server logs
- [ ] No stack traces exposed to users

### 9. Blockchain Security (if applicable)
- [ ] Wallet signatures verified
- [ ] Transaction details validated
- [ ] Balance checks before transactions
- [ ] No blind transaction signing

### 10. Dependency Security
- [ ] Dependencies up to date
- [ ] No known vulnerabilities (npm audit clean)
- [ ] Lock files committed
- [ ] Dependabot enabled on GitHub
- [ ] Regular security updates

## Security Patterns

### Secrets Management
```typescript
// ❌ NEVER
const apiKey = "sk-proj-xxxxx"

// ✅ ALWAYS
const apiKey = process.env.OPENAI_API_KEY
if (!apiKey) {
  throw new Error('OPENAI_API_KEY not configured')
}
```

### Input Validation
```typescript
import { z } from 'zod'

const CreateUserSchema = z.object({
  email: z.string().email(),
  name: z.string().min(1).max(100)
})

export async function createUser(input: unknown) {
  const validated = CreateUserSchema.parse(input)
  return await db.users.create(validated)
}
```

### SQL Injection Prevention
```typescript
// ❌ NEVER
const query = `SELECT * FROM users WHERE email = '${userEmail}'`

// ✅ ALWAYS
const { data } = await supabase
  .from('users')
  .select('*')
  .eq('email', userEmail)
```

### Authentication
```typescript
// ❌ WRONG: localStorage (vulnerable to XSS)
localStorage.setItem('token', token)

// ✅ CORRECT: httpOnly cookies
res.setHeader('Set-Cookie',
  `token=${token}; HttpOnly; Secure; SameSite=Strict`)
```

## Security Testing

### Automated Security Tests
```typescript
// Test authentication
test('requires authentication', async () => {
  const response = await fetch('/api/protected')
  expect(response.status).toBe(401)
})

// Test input validation
test('rejects invalid input', async () => {
  const response = await fetch('/api/users', {
    method: 'POST',
    body: JSON.stringify({ email: 'not-an-email' })
  })
  expect(response.status).toBe(400)
})
```

## Pre-Deployment Security Checklist

Before ANY production deployment:

- [ ] **Secrets**: No hardcoded secrets, all in env vars
- [ ] **Input Validation**: All user inputs validated
- [ ] **SQL Injection**: All queries parameterized
- [ ] **XSS**: User content sanitized
- [ ] **CSRF**: Protection enabled
- [ ] **Authentication**: Proper token handling
- [ ] **Authorization**: Role checks in place
- [ ] **Rate Limiting**: Enabled on all endpoints
- [ ] **HTTPS**: Enforced in production
- [ ] **Security Headers**: CSP, X-Frame-Options configured
- [ ] **Error Handling**: No sensitive data in errors
- [ ] **Logging**: No sensitive data logged
- [ ] **Dependencies**: Up to date, no vulnerabilities
- [ ] **Row Level Security**: Enabled in Supabase
- [ ] **CORS**: Properly configured
- [ ] **File Uploads**: Validated (size, type)
- [ ] **Wallet Signatures**: Verified (if blockchain)

## Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Next.js Security](https://nextjs.org/docs/security)
- [Supabase Security](https://supabase.com/docs/guides/auth)
- [Web Security Academy](https://portswigger.net/web-security)

## Related Files

- `SKILL.md` - Full skill documentation with detailed examples
- [Security Reviewer Agent](../../agents/security-reviewer.md) - Agent that performs security reviews

---

**See also:**
- [Main README](../../README.md) - Overview of repository
- [Agents](../../agents/security-reviewer.md) - Security reviewer agent
- [Rules](../../rules/security.md) - Security rules
