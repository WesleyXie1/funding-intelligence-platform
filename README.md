# Proposed Process with Gemini Agent Interface

## Step 1. Funding Opportunity Input through Gemini Agent

Users interact with the system through a Gemini-based agent interface and provide a federal funding opportunity URL (e.g., NSF, NIH, DOE) or funding text. The Gemini agent serves as the conversational front end, collecting funding information and forwarding it to the backend matching engine.

The system extracts and processes key information from the funding announcement, including the program description, research priorities, eligibility requirements, deadlines, and major topic areas. If automatic webpage extraction fails, the agent prompts the user to provide the funding text manually.

---

## Step 2. Funding Profile Construction

The extracted funding text is processed by a large language model to construct a structured funding profile.

The model identifies key information such as:

* Research domains
* Methodologies
* Target populations
* Application areas
* Eligibility constraints
* Strategic priorities

The output includes a concise funding summary, research themes, methodological keywords, target areas, eligibility notes, and faculty-relevant concepts for downstream analysis.

---

## Step 3. Faculty Database Retrieval

The system retrieves faculty information from a curated faculty database.

Faculty profiles may include:

* Faculty name
* Department and affiliations
* Research interests
* Faculty webpage
* Selected publications
* Recent research topics
* Research centers and institutes

This database serves as the primary knowledge source for faculty matching and recommendation.

---

## Step 4. Embedding-Based Faculty Retrieval

The structured funding profile and faculty research profiles are converted into numerical embeddings using a pretrained language model.

Embeddings represent the semantic meaning of text in a high-dimensional vector space, allowing conceptually related topics to be matched even when different terminology is used.

The system computes cosine similarity between the funding embedding and each faculty embedding:

Similarity(F,P) = (F · P) / (||F|| ||P||)

where:

* F = funding opportunity embedding
* P = faculty profile embedding

This retrieval stage enables efficient screening across a large faculty database and identifies an initial pool of potentially relevant faculty members.

Unlike traditional keyword-based matching, the embedding-based approach captures broader semantic relationships between funding priorities and faculty research interests.

Faculty members with the highest similarity scores are selected for further evaluation.

---

## Step 5. Faculty Ranking with Weighted Scoring

After the retrieval stage, the system computes an initial faculty match score using a weighted scoring framework:

Score = 0.40 × Semantic Similarity
+ 0.25 × Research Interest Overlap
+ 0.25 × Publication Relevance
+ 0.10 × Affiliation Fit

Components include:

* Semantic Similarity (40%)
* Research Interest Overlap (25%)
* Publication Relevance (25%)
* Department or Center Affiliation Fit (10%)

This step generates an initial ranked list of faculty members most relevant to the funding opportunity.

---

## Step 6. LLM-Based Reranking

The top-ranked faculty candidates are then reviewed by a large language model such as GPT.

Rather than relying solely on embedding similarity scores, GPT evaluates:

* Topical fit
* Methodological fit
* Application fit
* Eligibility fit
* Likelihood of faculty interest

The model assigns a refined relevance score and generates a concise explanation describing why each faculty member is or is not a strong match.

This stage functions as a second-level expert review layer that improves recommendation quality and interpretability.

---

## Step 7. Evidence-Based Recommendation

For each recommended faculty member, the system generates an evidence-based justification.

Recommendations may reference:

* Shared research themes
* Overlapping methodologies
* Relevant publication topics
* Matching application domains
* Strategic alignment with funding priorities

The objective is not only to identify relevant faculty members but also to provide transparent reasoning behind each recommendation.

---

## Step 8. Mail Merge Draft Generation

After the final faculty ranking is produced, the system generates outreach drafts.

Supported outputs include:

* Group emails for broader faculty audiences
* Personalized outreach emails for highly matched faculty members

Each draft includes:

* Funding opportunity information
* Match rationale
* Suggested next steps
* Contact information for the Office of Research Development

---

## Step 9. Gemini Agent Response and User Review

The backend matching engine returns ranked faculty recommendations, evidence summaries, and email drafts to the Gemini agent.

The Gemini interface presents results conversationally and supports follow-up interactions such as:

* "Why was this faculty member ranked highly?"
* "Generate a shorter version of the email."
* "Show only Statistics faculty."
* "Export results for mail merge."

This enables users to iteratively refine recommendations through natural language interaction.

---

## Step 10. Human Review and Export

The system does not automatically send emails.

Instead, it produces a reviewable set of:

* Faculty rankings
* Recommendation explanations
* Outreach drafts

Users may export results to CSV, Excel, or mail merge formats for final review and distribution.

Human users remain responsible for final decisions, editing, and communication.

---

# System Architecture Summary

Gemini Agent Interface

↓

Funding Opportunity Input

↓

Funding Profile Construction

↓

Faculty Database Retrieval

↓

Embedding-Based Faculty Retrieval

↓

Weighted Faculty Ranking

↓

LLM-Based Reranking

↓

Evidence-Based Recommendation

↓

Mail Merge Draft Generation

↓

User Review and Export

---


