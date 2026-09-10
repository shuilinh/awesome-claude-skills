# Strict Verification Templates (Collaboration-Reinforced)

## 1. Recommended User Bug Report Format (copyable, send to the AI)

```
【Bug Report】
1. Exact steps (step by step):
   -
   -
   -
2. Result actually observed:
3. Expected result:
4. Where / which feature is involved:
5. Does it reproduce every time? Any specific conditions?
6. Are other related features affected? (e.g. state out of sync, feedback missing, settings not taking effect, etc.)
```

## 2. Understanding Confirmation the AI Must Do First

After receiving a bug report, the AI should first output:

```
My understanding of the problem is:
- Operation path: ...
- Actual result: ...
- Expected result: ...
- Features involved: ...
- Possible collaboration impact: ...
Please confirm whether my understanding is correct.
```

## 3. Strict Review Report Structure

```
【Strict Review Report】

Against checklist items:

1. [Item name]
   - Verification method: ...
   - Observed result: ...
   - Meets acceptance criterion: yes / no / cannot verify
   - Problem or gap: ...

2. ...

Cross-feature collaboration verification (must include relevant items):
- Journey / scenario: ...
  - Steps: ...
  - Observed: ...
  - Matches expected collaborative behavior: yes / no / cannot verify
  - Problem: ...

Problems found proactively:
- ... (prioritize reporting state out of sync, inconsistent feedback, error silos, settings not reacting, baseline capabilities decoupled from business logic, etc.)

Items that cannot be verified, and why:
- ...

(Writing only "all green" or "no problem" is forbidden)
```
