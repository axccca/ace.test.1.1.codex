# Personeelsnetwerk Master Prompt - Quick Reference

## AI Model Selection

| Task Type | Primary Model | Fallback | Cost |
|-----------|---------------|----------|------|
| Compliance/Legal/GDPR | Claude | ChatGPT | Medium |
| Content Creation | ChatGPT | Claude | Medium |
| Lead Generation | ChatGPT | Gemini | Medium |
| Data Analysis | Gemini | ChatGPT | Low-Med |
| Code/Technical | DeepSeek | ChatGPT | Low |
| Real-time/Trends | Grok | ChatGPT | Low |
| Strategic Decisions | K1/Reasoning | Claude | High |

## Section Files for n8n Context Injection

```
prompts/sections/
├── 00_IDENTITY.txt          # Core identity (always include)
├── 01_AI_ORCHESTRATION.txt  # Model routing rules
├── 04_SEO_CONTENT.txt       # Content/SEO tasks
├── 05_SOCIAL_MEDIA.txt      # Social media tasks
├── 06_LEAD_GENERATION.txt   # Sales/leads tasks
├── 07_OPERATIONS.txt        # Dispatch/shifts tasks
├── 11_WHATSAPP.txt          # Communication tasks
├── 12_BILLING.txt           # Finance/invoicing tasks
├── 13_COMPLIANCE.txt        # Legal/GDPR tasks
└── 18_BUDGET.txt            # Cost optimization
```

## Key Metrics (North Star)

**Primary:** Profitable filled shifts (margin-positive, no SLA breach)

| Metric | Target |
|--------|--------|
| Time to fill | < 4 hours |
| Fill rate | > 95% |
| Gross margin | > 25% |
| Client LTV | > €5,000 |
| CAC | < €200 |
| Staff churn (90d) | < 30% |
| Client churn (180d) | < 15% |

## Lead Scoring Quick Reference

| Score | Category | Action |
|-------|----------|--------|
| ≥ 80 | Hot | Call within 5 min + WhatsApp |
| 50-79 | Warm | SDR sequence within 1 hour |
| < 50 | Nurture | Email drip + retargeting |

## Shift Fill Tiers

1. **Auto-match** (immediate): reliability × skills × location × cost
2. **WhatsApp broadcast** (15 min): qualified pool
3. **Partner network** (internal exhausted)
4. **Human dispatcher** (complex/VIP)

## Pricing Modifiers

| Condition | Modifier |
|-----------|----------|
| Night shift | +25% |
| Weekend | +15% |
| Holiday | +50-100% |
| Last-minute (<24h) | +20% |
| Surge | Dynamic |

## Compliance Checklist

- [ ] WAADI registration current
- [ ] SNA certification valid
- [ ] CAO rates applied correctly
- [ ] Consent captured before outreach
- [ ] GDPR rights workflows active
- [ ] Security incidents reported <24h

## Usage in n8n

```javascript
// Example: Load context for operations task
const context = await $getWorkflowStaticData('global');
const operationsContext = context.prompts['07_OPERATIONS'];

// Inject into AI request
const systemPrompt = `${identityContext}\n\n${operationsContext}`;
```

## Usage in Claude Code / VSC

```
// For complex tasks: Load full MASTER_PROMPT_v2.0.md
// For focused tasks: Load relevant section from prompts/sections/

// Example: Compliance review
// Load: 00_IDENTITY.txt + 13_COMPLIANCE.txt
```

## Version Control

- **Current Version:** 2.0
- **Last Updated:** 2024-12-20
- **Location:** GitHub: axccca/ace.test.1.1.codex/prompts/
