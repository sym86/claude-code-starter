# /security-review — Audit a diff or file for security issues

## Inputs
Either a diff (default: `git diff main...HEAD`) or a specific file/path
I point you at. If I don't specify, audit the current branch's diff
against main.

## Steps

### 1. Scope check
- List the files/paths you'll audit and the lines-of-code count.
- If the diff is larger than ~500 LOC, ask me which area to focus on
  first rather than skimming everything shallowly.

### 2. Run the checklist
For each finding, output: severity (🔴 critical / 🟠 high / 🟡 medium /
🔵 low), file:line, the issue, and the minimal fix.

**Secrets & credentials**
- Any hard-coded API keys, tokens, passwords, connection strings,
  private keys, or `.pem` content (even in tests or fixtures).
- Secrets in URLs, query params, log statements, or error messages.
- `.env*` files staged for commit. Verify `.gitignore` covers them.

**Input handling**
- Untrusted input (HTTP body/query/params, file uploads, env, user
  DB content) reaching: SQL queries, shell commands, `eval`/`Function`,
  template renderers, file paths, HTTP clients (SSRF), or redirects.
- Missing validation at trust boundaries. Schema validation should
  happen before business logic, not interleaved with it.

**Authn / authz**
- New routes/handlers without an auth check.
- Authorization checks that compare to user-supplied IDs without
  verifying ownership.
- Tokens stored or transmitted insecurely (localStorage for sensitive
  tokens, non-httpOnly cookies for session, etc.).
- Password handling: plain comparison, weak hashing, missing rate limits.

**Injection & deserialization**
- String concatenation building SQL, shell, LDAP, or HTML.
- `JSON.parse` / `yaml.load` / `pickle.loads` on untrusted input
  without safe loaders.
- Unsafe deserialization of session/cookie data.

**Crypto**
- MD5/SHA1 for anything security-relevant.
- ECB mode, missing IVs, reused nonces, predictable randomness
  (`Math.random` for tokens).
- Custom crypto primitives — flag any roll-your-own.

**Dependencies & supply chain**
- New dependencies added: are they widely used, recently updated, from
  a known maintainer? Flag anything with <100 weekly downloads or
  recent ownership change.
- `postinstall` scripts in new deps.

**Logging & error handling**
- PII, tokens, or full request bodies being logged.
- Stack traces or DB errors exposed to end users.
- Error messages that reveal account existence, file paths, or
  internal IDs.

**Web-specific (if applicable)**
- Missing CSRF protection on state-changing endpoints.
- CORS configured with `*` for credentialed requests.
- Missing rate limiting on auth/expensive endpoints.
- `dangerouslySetInnerHTML`, raw `v-html`, or equivalent without
  sanitization.

### 3. Summary
End with one of:
- ✅ "No issues found" — the diff is clean.
- ⚠️ "Issues found, see above" + a top-3 prioritized fix list.
- 🛑 "Blocker — do not merge" + the specific critical finding(s).

## Constraints
- Cite file:line for every finding. No findings without a location.
- Don't invent vulnerabilities. If unsure whether something is exploitable,
  say so and ask before flagging it as critical.
- Don't write the fixes yourself in this command — output the diagnosis;
  fixes go through normal review.
- Never quote a real secret you find — describe it ("a 32-char hex string
  that looks like an API key on line 14") so I can rotate it without it
  appearing in logs.
