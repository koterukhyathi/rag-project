1. Project Overview
1.1 Background
Airport wheelchair assistance operations are governed by strict federal regulations under 14 CFR Part 382 (the Air Carrier Access Act). Agents on the ground must answer service eligibility questions in real time: what services is a passenger entitled to, what restrictions apply, and what regulations back those entitlements?

Existing knowledge is locked in PDF regulation documents and static reference cards. There is no unified natural-language interface that lets agents query this information quickly and accurately. This project builds one using Retrieval-Augmented Generation (RAG).
 
1.2 Project Goal
Build a RAG system that allows airport operations staff to query passenger assistance policy in natural language, receiving accurate, regulation-cited answers grounded in the passenger_assistance_corpus.json knowledge base — with no hallucination.
 
1.3 Scope — Current Implementation
The current implementation covers the policy knowledge base only, using the passenger_assistance_corpus.json file as the single source of truth. The system answers eligibility questions, service entitlement questions, regulatory questions, and SLA questions across all 12 disability profiles.

1.4 Key Design Decisions
• Schema-aware chunking instead of RecursiveCharacterTextSplitter — preserves semantic boundaries in structured JSON
• Three chunks per profile (identity / services / compliance) — each chunk answers a distinct query type
• Metadata filtering on every Pinecone search — prevents retrieval noise across doc types and SSR codes
• Excluded services explicitly in page_content — enables the model to answer negative eligibility questions correctly
• Regulatory citations in compliance chunk — every answer can cite the governing regulation