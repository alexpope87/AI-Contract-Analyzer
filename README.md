# AI Contract Analyzer

AI-powered contract analysis prototype for extracting key contractual information and identifying potential areas of attention.

## Problem

Reviewing contracts manually can be time-consuming.

Important information such as payment terms, duration, renewal conditions, termination clauses, penalties and obligations is often distributed across different sections of a document.

The initial review therefore requires users to read and interpret a potentially long document before they can organize the information they need.

## Solution

AI Contract Analyzer is a lightweight web application that uses AI to extract and structure relevant information from PDF contracts.

The goal is not to replace legal professionals or provide legal advice.

Instead, the application is designed to reduce the time required for an initial review by transforming unstructured contract text into a structured overview.

## How It Works

```text
PDF Contract
     ↓
Supabase Storage
     ↓
PDF Text Extraction
     ↓
Gemini AI Analysis
     ↓
Structured JSON
     ↓
Results Dashboard

1. Upload

The user uploads a PDF contract.

The document is stored in a private Supabase Storage bucket.

2. Text Extraction

The application extracts the text from the uploaded PDF on the server.

If the PDF is unreadable or contains no extractable text, the process stops and an error is displayed.

3. AI Analysis

The extracted text is sent to Gemini through a server-side API integration.

The AI is instructed to focus on factual extraction rather than generating a generic summary.

4. Structured Output

The AI returns structured information covering:

Contract type
Parties
Purpose
Start and end dates
Duration
Financial terms
Renewal conditions
Termination conditions
Key clauses
Attention Points

Missing information is not invented and can be returned as Not specified.

5. Results Dashboard

The structured output is displayed in a simple dashboard designed to make the most relevant contractual information easier to review.

AI Design Principles

The project uses several principles to improve reliability:

Structured extraction instead of generic summarization
No unsupported assumptions
Explicit handling of missing information
Factual extraction over legal interpretation
No numerical risk score
Attention Points based on actual contract content
Human review remains necessary
Technology
Frontend: Lovable
Backend / Storage: Supabase
PDF Processing: Server-side PDF text extraction
AI: Google Gemini API
Output: Structured JSON
Deployment: Lovable
MVP Scope
Included
PDF upload
Private document storage
PDF text extraction
AI-powered contract analysis
Structured JSON output
Contract information dashboard
Attention Points
Basic error handling
Not Included
Legal advice
Automated legal decisions
Contract negotiation
Contract generation
OCR for scanned documents
Multi-contract comparison
User accounts
Collaboration
Advanced risk scoring
Testing

The application was tested end-to-end using a real PDF contract.

The test verified:

PDF upload
Supabase storage
Text extraction
Gemini analysis
Structured output
Missing information handling
Attention Points
Error handling
Successful build

Detailed testing and validation are documented in:

docs/05-testing.md

Project Documentation

The project was designed and documented incrementally:

Problem Definition
Solution Design
AI Workflow
User Interface
Testing & Validation
Limitations

This is an MVP and should be considered an analysis aid rather than a legal tool.

AI-generated results may contain errors or misunderstandings. Users should verify relevant information against the original contract and seek professional legal advice when appropriate.

The current version works with PDFs containing extractable text and does not include OCR for scanned documents.

Lessons Learned

Building an AI document-analysis workflow requires more than connecting an LLM API.

Reliable results depend on the combination of:

document processing
structured prompting
controlled AI output
secure API integration
explicit handling of missing information
validation against real documents

The project also highlighted the importance of testing AI-generated information against the original source document rather than assuming that a technically successful AI response is necessarily accurate.
