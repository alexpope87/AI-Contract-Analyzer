# AI Contract Analyzer — AI Workflow

## 1. Objective

The AI component is responsible for analyzing the text extracted from a contract and converting unstructured contractual information into a predefined structured format.

The objective is not to generate a generic summary, but to extract specific information that can be displayed consistently by the application.

## 2. AI Workflow

The workflow is:

> Contract PDF → Text Extraction → AI Analysis → Structured JSON → Application UI

### Input

The initial input is the text extracted from a PDF contract.

### Processing

The extracted text is sent to the AI model together with instructions defining:

* What information to extract
* How the information should be structured
* How missing information should be handled
* Which clauses should be highlighted as attention points

### Output

The AI returns structured JSON.

## 3. Output Schema

The initial MVP will use the following structure:

```json
{
  "contract_type": "",
  "parties": [],
  "purpose": "",
  "start_date": "",
  "end_date": "",
  "duration": "",
  "financial_terms": {
    "amount": "",
    "payment_frequency": "",
    "payment_deadline": "",
    "penalties": ""
  },
  "renewal": {
    "automatic": false,
    "conditions": "",
    "notice_period": ""
  },
  "termination": {
    "conditions": "",
    "notice_period": ""
  },
  "key_clauses": [],
  "attention_points": []
}
```

## 4. Field Definitions

### Contract Information

**contract_type**

The type of contract identified by the AI.

Examples:

* Service Agreement
* Employment Agreement
* Lease Agreement
* Non-Disclosure Agreement

**parties**

The individuals or organizations involved in the contract.

**purpose**

A short description of the main purpose of the agreement.

**start_date**

The contract start date, if explicitly stated.

**end_date**

The contract end date, if explicitly stated.

**duration**

The stated duration of the contract.

### Financial Terms

**amount**

Main contractual amount, if applicable.

**payment_frequency**

For example:

* Monthly
* Quarterly
* Annually
* One-time

**payment_deadline**

Relevant payment deadlines.

**penalties**

Financial penalties or additional charges explicitly identified in the contract.

### Renewal

**automatic**

Whether the contract appears to include automatic renewal.

**conditions**

Conditions associated with renewal.

**notice_period**

Notice required to prevent or modify renewal.

### Termination

**conditions**

Conditions under which the contract can be terminated.

**notice_period**

Required notice period.

### Key Clauses

A list of relevant contractual clauses identified by the AI.

Each item should contain a short description rather than reproducing large sections of the original document.

### Attention Points

Potential areas that may deserve closer review.

Examples include:

* Automatic renewal
* Long termination notice
* Significant penalties
* Unusual payment conditions
* Important obligations
* Restrictions

## 5. Handling Missing Information

The AI should not invent information that is not present in the document.

If a field cannot be reliably identified, it should return an empty value or explicitly indicate that the information was not found.

For example:

```json
{
  "end_date": "",
  "duration": "Not specified"
}
```

The system should distinguish between:

* Information explicitly found
* Information that was not found
* Information that is ambiguous

## 6. AI Reliability Principle

The AI should prioritize factual extraction from the document over interpretation.

When information is ambiguous, the system should indicate the uncertainty rather than presenting an assumption as a fact.

## 7. Human Oversight

The AI output is intended to support an initial document review.

It should not be presented as legal advice or as a definitive interpretation of contractual obligations.

Users should verify important information against the original document and seek professional legal advice when appropriate.

## 8. Future Improvements

Potential future improvements include:

* Source references linking each extracted item to the relevant section of the contract
* Confidence indicators
* Contract comparison
* Clause-level analysis
* Support for additional document formats
* More advanced classification
* Human feedback on AI results
