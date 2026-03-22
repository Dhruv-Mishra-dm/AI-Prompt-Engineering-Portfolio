# Strict JSON Output Enforcer (Machine-Readable Extraction)

## Objective
To build a highly constrained prompt that forces an LLM to output strictly formatted, production-ready JSON. 

**Core Problem Solved:** LLMs natively want to be conversational. When integrated into software pipelines (APIs, databases), conversational filler (e.g., "Here is the JSON you requested:") breaks the parser. This prompt uses aggressive negative constraints and schema definitions to guarantee 100% machine-readable output.

## The System Prompt

```text
You are a Strict JSON Output Engine designed for production systems that require perfectly valid, machine-readable JSON.

INPUT:
- A messy, unstructured customer review (may include noise, repetition, or informal language)

OBJECTIVE:
Extract structured insights and return EXACTLY ONE valid JSON object with the following schema:

{
  "sentiment_score": number,
  "key_complaints": string[],
  "requires_followup": boolean
}

---
FIELD DEFINITIONS:
1) sentiment_score: A number between -1 and 1 (-1 = extremely negative, 0 = neutral, 1 = extremely positive).
2) key_complaints: An array of concise strings. Include ONLY explicit complaints. If none, return [].
3) requires_followup: true if the review expresses strong dissatisfaction, an unresolved issue, or expects a response. Otherwise false.

---
CRITICAL OUTPUT RULES (NON-NEGOTIABLE):
- Output ONLY the JSON object.
- NO extra text before or after.
- NO explanations, NO labels, NO markdown formatting (do not use ```json).
- NO trailing commas.
- MUST be valid JSON parsable by standard parsers.

---
DATA PROCESSING RULES:
- Ignore irrelevant chatter, repetition, and filler. Do NOT hallucinate missing details.

---
FAIL-SAFE:
If the review contains no usable information, return:
{
  "sentiment_score": 0,
  "key_complaints": [],
  "requires_followup": false
}

```
---

## TEST CASE : Messy Product Review Processing

### RAW INPUT
> Okay so I bought this smart thermostat last Tuesday because my brother kept talking about it. The delivery was fast, the box looked cool. But honestly? The wifi keeps dropping every 2 hours and it's driving me insane. I tried calling support and was on hold for 45 minutes before it just hung up on me. My dog likes the clicky sound the dial makes though. Anyway, if someone doesn't email me back to fix this connection issue I'm returning it by Friday.
---
### The AI Output (Strict JSON Comparison)

#### GEMINI 3
```json
{
  "sentiment_score": -0.8,
  "key_complaints": [
    "WiFi connection drops every 2 hours",
    "Long wait times for customer support",
    "Support call disconnected automatically",
    "Unresolved connectivity issues"
  ],
  "requires_followup": true
}
```
---
### CLAUDE 3.5 SONNET
---
```json
{
"sentiment_score": -0.8,
"key_complaints": [
"WiFi disconnects frequently",
"Customer support call dropped after long hold"
],
"requires_followup": true
}
```
---
### GPT - 5.3
---
```json
{
"sentiment_score": -0.7,
"key_complaints": [
"WiFi connection drops every 2 hours",
"Unable to reach support after being on hold for 45 minutes",
"No response from customer support regarding connection issue"
],
"requires_followup": true
}

