# Prompt Package Output Template

Use this template when the user wants a deliverable they can hand to a product, design, or engineering team.

## 1. Goal and placement

- Product:
- Feature:
- User:
- Desired outcome:
- Product stage:
- Prompt role:
- Assumptions:

## 2. Research trace

| Source | Exact or analogous | Relevant pattern | Evidence label | Limitation |
|---|---|---|---|---|
|  |  |  |  |  |

## 3. Workflow contract

| Item | Definition |
|---|---|
| Trigger |  |
| Required inputs |  |
| Optional inputs |  |
| Main decisions |  |
| Tools/data |  |
| Intermediate state |  |
| Handoff |  |
| Completion criteria |  |
| Failure behavior |  |

## 4. Prompt artifacts

### System Prompt

```text
<copyable system prompt>
```

### User Prompt Template

```text
<copyable user prompt template>
```

### Optional Tool / Evaluator Prompt

```text
<copyable optional prompt>
```

## 5. Output contract

```json
{
  "status": "draft|needs_clarification|complete|blocked",
  "summary": "",
  "assumptions": [],
  "result": {},
  "uncertainties": [],
  "next_action": ""
}
```

## 6. Validation cases

| Case | Input condition | Expected behavior | Must not happen |
|---|---|---|---|
| Normal | Complete request |  |  |
| Missing input | Required field absent |  |  |
| Ambiguous | Multiple plausible goals |  |  |
| Revision | User changes one constraint |  |  |
| Failure | Tool or data unavailable |  |  |
