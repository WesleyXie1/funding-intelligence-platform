# funding intelligence platform
AI powered faculty funding matching and outreach platform using embeddings, LLM reranking, and Gemini integration.


Proposed Process with Gemini Agent Interface


## Step 1. Funding Opportunity Input through Gemini Agent
The user interacts with the system through a Gemini-based agent interface and provides a federal funding opportunity URL (e.g., NSF, NIH, or DOE) or funding text. The Gemini agent serves as the conversational front end, collecting the funding information and forwarding it to the backend matching engine. The system then extracts and processes key content from the funding announcement, including the program description, research priorities, eligibility requirements, deadlines, and major topic areas. If the webpage cannot be parsed automatically, the agent prompts the user to provide the funding text manually.

## Step 2. Funding Theme Extraction (transfer to machine code)
The extracted funding text is processed by a large language model to identify the core themes of the opportunity. These may include research domains, methods, target populations, application areas, eligibility constraints, and strategic priorities.
The output is a structured funding profile, including a short summary, key research themes, methods, target areas, eligibility notes, and potential faculty-relevant keywords.

Step 3. Faculty Database Retrieval
The faculty database contains public information such as faculty name, department, research interests, faculty webpage, selected publications, and recent research topics.

Step 4. Embedding Retrieval Using Cosine Similarity (transfer the non direct wording to keyword for matching)
The structured funding profile and faculty research profiles are converted into numerical embeddings using a pretrained language model. These embeddings capture the semantic meaning of the text in a high-dimensional vector space, allowing conceptually related topics to be matched even when different terminology is used.
The system then computes the cosine similarity between the funding embedding and each faculty embedding. Cosine similarity measures the alignment between two embeddings and serves as an estimate of semantic relevance.
This retrieval stage enables efficient screening across a large faculty database and identifies an initial pool of potentially relevant faculty members. Rather than relying solely on exact keyword matches, the embedding-based approach can detect broader conceptual relationships between funding priorities and faculty research interests.
Faculty members with the highest similarity scores are selected as candidates for further evaluation in the ranking and reranking stages.


Step 5. Faculty Ranking with Weighted Scoring (to save token)
After the initial embedding retrieval, the system calculates a weighted match score for each faculty member. The score combines multiple components, such as:
Semantic similarity between the funding and faculty profile: 40%
Research interest overlap: 25%
Recent publication relevance: 25%
Department or center affiliation fit: 10%
This produces an initial ranked list of faculty members who are likely to be relevant to the opportunity.

Step 6. LLM-Based Reranking with GPT
The top-ranked faculty candidates are then reviewed by a large language model, such as GPT. Instead of relying only on cosine similarity, GPT reads the funding summary, the faculty research profile, and recent publication information.
GPT evaluates the match based on topical fit, methodological fit, application fit, eligibility fit, and likelihood of faculty interest. It assigns a refined score and provides a short explanation for why the faculty member is or is not a strong match.
This step acts as a second-stage expert review after the embedding-based retrieval stage.

Step 7. Evidence Based Recommendation
For each recommended faculty member, the system provides an evidence-based explanation. This includes the specific overlap between the funding opportunity and the professor’s research, such as shared keywords, related methods, relevant publication topics, or matching application areas.

Step 8. Mail Merge Draft Generation
After the final faculty list is produced, the system generates outreach drafts. It can create a group email for a broader set of faculty or personalized emails for highly matched faculty members.
The draft email includes the funding opportunity, the reason it may be relevant, and a short call to action, such as inviting the faculty member to contact the Office of Research Development for support.

Step 9. Gemini Agent Response and User Review
The backend returns the ranked faculty list, match explanations, and email drafts to the Gemini agent. The Gemini agent presents the results in a user-friendly format and allows the user to ask follow-up questions, such as:
“Why was this professor ranked highly?”
“Generate a shorter version of the group email.”
“Only include faculty from the Statistics Department.”
“Export this list for mail merge.”


Step 10. Human Review and Export
The final output is not sent automatically. Instead, the system produces a reviewable faculty ranking, match explanations, and email drafts. Users can export the results to CSV, Excel, or a mail merge format for manual review and final editing.
The human user remains responsible for final decisions, editing, and sending.

System Architecture Summary
Gemini Agent Interface
→ User submits funding URL or funding text
→ Gemini sends request to backend API
→ Python matching engine extracts and summarizes funding content
→ Embedding retrieval identifies candidate faculty
→ Weighted scoring ranks faculty
→ GPT reranks and explains matches
→ Email drafts are generated
→ Gemini presents results conversationally
→ User reviews and exports results



