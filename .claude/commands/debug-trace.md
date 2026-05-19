# /debug-trace — Diagnose an error or stack trace

## Inputs
I'll paste an error message, stack trace, log snippet, or describe a
bug. If I don't include reproduction steps, ask for them before
hypothesizing.

## Steps

### 1. Capture context
- Quote the exact error message and the top 5 frames of the stack
  (or the most relevant log lines).
- Identify the failing file:line and the function/handler involved.
- Note the runtime: Node version, env (dev/staging/prod), recent deploys.

### 2. Reproduce locally (don't skip)
- Propose the minimal command or test case that triggers the bug.
- If you can't reproduce it from the info given, list the 1–3 questions
  whose answers would unlock reproduction, and stop.

### 3. Localize
- Read the failing file and its direct callers.
- Identify whether the cause is: (a) bad input, (b) unhandled state,
  (c) race/async ordering, (d) external dependency, (e) config/env,
  (f) recent code change. Pick one.

### 4. Hypothesize
- State the most likely root cause in one sentence.
- List up to 2 alternative hypotheses, each with what evidence would
  rule it out.

### 5. Verify before fixing
- Propose the smallest change that would prove the hypothesis
  (a log line, a test, a tweaked input). Run it.
- Do not write the fix yet.

### 6. Propose the fix
- Once verified, propose the **minimum diff** that solves the root
  cause — not the symptom.
- Include a regression test that would have caught the bug.
- Note any related code that has the same bug pattern.

## Constraints
- Never paper over the symptom (e.g. try/catch that just swallows the
  error). Fix the cause.
- If the bug only happens in production, refuse to "fix and hope" —
  propose more logging/telemetry first.
- Cite file:line for every claim about the code.
- If you can't reach a confident hypothesis, say so and ask for more
  information rather than guessing.
