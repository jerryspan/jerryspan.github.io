---
layout: page
permalink: /thesis/
title: thesis
description: 
nav: true
nav_order: 6
---

This is a non-exhaustive list of topics available to DACS bachelor/master students. Please note the following before you send me an email or select me as a supervisor.

+ You will need to read and understand many (recent) research papers.
+ You are expected to be independent and self-motivated but also report, update and “teach” me new things as well
+ I will push you to do good work and provide the needed conditions for it.
+ I won’t pressure with deadlines, etc.
+ Don't send me emails written with an LLM. If you insist, send me the prompt.
+ Don't create presentations with Claude (or other LLMs). It's easy for me to figure it out.
+ You need to know how to program and love (unconditionally) to program. I don't care how you program, but I expect that you know what your code is doing.
+ You will need to be able to “get things to work”.
+ It will be mostly hard work but you will be reimbursed by the quality results (most of the time…)
+ My research interests are in applied ML and NLP in the topics highlighted below.
+ I am open to working on other Data Mining/Machine Learning areas but you have to convince me they are interesting.

<!--
<details markdown="1">
<summary>
</summary>
</details>
-->

<details markdown="1">
<summary>
Cross-lingual retrieval of EU legal text
</summary>
Draws on existing work on legal retrieval benchmarks (e.g. BSARD, Louis & Spanakis 2022) and multilingual dense retrieval (e.g. BGE-M3, Chen et al. 2024), and applies them to the setting where a user queries in one EU language and the relevant legal documents are in another. Multilingual legal retrieval is a real gap: most legal IR benchmarks are monolingual, while EU legal practice is inherently multilingual.

### Objective (pick some, or zoom in)
- Compare lexical (BM25), translation-based (translate the query, then BM25), and multilingual dense retrieval on cross-lingual legal retrieval.
- Quantify the cross-lingual gap: how much retrieval quality drops when query and document languages differ, per language pair.
- Test whether hybrid retrieval (BM25 + dense, fused) closes the gap, and whether legal-domain fine-tuning helps over general multilingual models.
- Analyse failure cases, e.g. legal concepts with no exact equivalent across legal systems.

### How
- Data: [EUR-Lex](https://eur-lex.europa.eu/content/help/data-reuse/reuse-contents-eurlex-details.html) as the main corpus (the same act exists in up to 24 languages, which gives cross-lingual relevance labels for free), plus [LEXTREME](https://huggingface.co/datasets/joelniklaus/lextreme) for additional multilingual legal text.
- Task construction: (a) title or summary in language A, relevant document is the same act in language B; (b) topic-based relevance via EuroVoc labels; (c) optionally, real questions from BSARD (French), machine-translated into other languages as a smaller, harder test set.
- Systems: BM25 (Lucene/OpenSearch/Pyserini), 3-5 multilingual embedding models (multilingual-e5, LaBSE, BGE-M3), an MT pipeline, and hybrid fusion (RRF).
- Evaluation: nDCG@10, Recall@k, and MRR, reported per language pair. Qualitative review of a sample of failures with a legal-expert colleague.
- Optional: fine-tune one embedding model on in-domain legal pairs.

### Outputs
- A reproducible evaluation pipeline and a cross-lingual legal retrieval benchmark (query sets and relevance judgments).
- A quantitative comparison of methods per language pair, with recommendations for multilingual legal search.

# Prerequisites
Python, basic NLP and IR (BM25, embeddings), some experience with Hugging Face or sentence-transformers. Legal knowledge is not required.

# References (indicative)
- Chalkidis, I., Fergadiotis, M., & Androutsopoulos, I. (2021). MultiEURLEX: a multi-lingual and multi-label legal document classification dataset for zero-shot cross-lingual transfer. EMNLP 2021.
- Louis, A., & Spanakis, G. (2022). A statutory article retrieval dataset in French. ACL 2022 (and more recent papers of Antoine Louis)
- Chen, J., et al. (2024). BGE M3-Embedding: multi-lingual, multi-functionality, multi-granularity text embeddings. arXiv:2402.03216.
- Thakur, N., et al. (2021). BEIR: a heterogeneous benchmark for zero-shot evaluation of information retrieval models. NeurIPS Datasets and Benchmarks.
- Niklaus, J., Matoshi, V., Rani, P., Galassi, A., Stürmer, M., & Chalkidis, I. (2023). LEXTREME: a multi-lingual and multi-task benchmark for the legal domain. Findings of EMNLP 2023. https://arxiv.org/abs/2301.13126
</details>


<details markdown="1">
<summary>
Hybrid legal case similarity (citations plus semantics)
</summary>
At Maastricht Law and Tech Lab we have the Case Law Explorer platform (https://app.caselawexplorer.tech/), where you can explore legal cases on the basis of which case cites which previous ones. That approach only takes into account network dynamics (citations). We would like to add the option of semantic text similarity and on precedent retrieval benchmarks such as ECtHR-PCR (Santosh et al. 2024) and apply a fusion framework to court decisions. Citation links are precise but sparse, while text similarity covers every case but can miss doctrinal links, so the question is how best to combine them.

### Objective (pick some, or zoom in)
- Compare citation-only, semantic-only, and hybrid similarity for recommending related cases.
- Compare fusion strategies: weighted score fusion, Reciprocal Rank Fusion (Cormack et al. 2009), and optionally a graph-embedding variant (node2vec/GraphSAGE combined with text embeddings).
- Study cold-start and temporal behaviour: how well does semantic similarity work for recent cases that nobody has cited yet, and how much does performance drift over time?
- Identify “disagreement cases” (high semantic and low citation similarity, and vice versa) as candidates for cross-jurisdiction recommendations.
- Optional: check for same-language bias in multilingual embeddings when comparing cases across languages.

### How
- Data: [ECtHR-PCR](https://huggingface.co/datasets/RashidHaddad/ECTHR-PCR) as the primary dataset (ready-made citation ground truth), optionally extended with CJEU decisions from EUR-Lex.
- Citation extraction: for EUR-Lex/CJEU data, parse ECLI/CELEX identifiers and case references (regex plus simple NER), build the citation graph, and report extraction precision and recall. ECtHR-PCR already provides citation links, so extraction work can be limited to the extension corpus.
- Signals: (a) citation similarity; (b) semantic similarity (multilingual embeddings, with chunking and pooling for long judgments).
- Evaluation: hold out a subset of citation edges as ground truth and build the citation signal only from the remaining ones, to avoid circularity. Respect time ordering, so that a query case never uses citations from later cases. Complement this with a small manual relevance check of top-ranked results.
- Visualisation: overlay both signals in one network view (solid edges for citations, dashed for semantic neighbours).

### Outputs
- A pipeline that builds the citation graph and semantic similarity layer from public case law.
- A quantitative comparison of citation-only, semantic-only, and fused approaches, with analysis of cold-start, temporal, and disagreement cases.
- A small interactive overlay visualisation.

### Prerequisites
Python, NLP models, basic graph analysis, (legal) QA and Information Retrieval

References (indicative)
- Santosh, T.Y.S.S., Haddad, R., & Grabmair, M. (2024). ECtHR-PCR: a dataset for precedent understanding and prior case retrieval in the European Court of Human Rights. LREC-COLING 2024. https://aclanthology.org/2024.lrec-main.486/
- Santosh, T.Y.S.S., Olguín Nolasco, I. M., & Grabmair, M. LeCoPCR: Legal concept-guided prior case retrieval for European Court of Human Rights cases. https://arxiv.org/pdf/2501.14114
- Arosemena, G., van Dijck, G., & Moerland, R. (2026). Legal Network Analysis. (1.0.0 ed.) Maastricht University Press. https://doi.org/10.26481/mup.2606
- Van Kuppevelt, D., Van Dijck, G., & Schaper, M. (2020). Purposes and challenges of legal citation network analysis on case law. In Computational legal studies (pp. 265-292). Edward Elgar Publishing.

</details>


<details markdown="1">
<summary>
Linguistic Expression of Uncertainty vs. Overconfidence in LLM-Generated Legal Answers
</summary>

Draws on the existing/blooming work (e.g. Zhou/Rathi/Jurafsky's work on epistemic markers ("Navigating the Grey Area", Zhou et al. 2023; "Humans overrely on overconfident language models, across languages", Rathi et al. 2025)) and applies their framework to the legal QA domain, where miscalibrated confidence carries particularly high real-world stakes.

### Objective (some and you might pick more or zoom in)
- Determine whether LLMs answering legal questions linguistically signal their own uncertainty (hedges, epistemic markers like "I think", "it depends", "you should consult a lawyer") when they are in fact more likely to be wrong, or whether they default to confident-sounding phrasing regardless of correctness (linguistic overconfidence).
- Quantify the gap between a model's internal uncertainty (e.g. via output probabilities/self-consistency) and its expressed uncertainty (epistemic markers in the text) on legal questions specifically.
- Explore whether this over/under-expression pattern differs across languages/jurisdictions (e.g. English common-law vs. EU civil-law questions), extending the cross-linguistic calibration question from Rathi et al. to a single specialized domain. This depends a bit on the datasets we have available for legal QA.

### How
- Data: Select one or more legal QA datasets — e.g. English resources (LegalBench, CUAD-derived QA, existing bar-exam/legal-reasoning benchmarks) and/or others we curate locally at Law and Tech Lab (e.g. we have some smaller French and Dutch legal QA sets).
- Epistemic marker typology: Adapt Zhou et al.'s typology of certainty/uncertainty/evidential markers ("I'm sure", "I think", "according to X law") to the legal register (including hedges like "this may vary by jurisdiction", "consult a lawyer").
- Response generation: Query several LLMs (open + closed, and ideally at least one legal-domain-tuned model) on the legal QA set, collecting free-text answers.
- Labelling for correctness, epistemic markers, calibration etc. (depending on the scope): Score each answer against the dataset's gold answer/ground truth (automatic where possible, manual/expert review for a sampled subset given legal nuance). Automatically detect epistemic markers (lexicon/classifier-based, following Zhou et al.'s method) and correlate marker presence/type with answer correctness — testing whether confident phrasing appears disproportionately on wrong answers (the core "overconfidence" finding to replicate in the legal domain). Where available, compare expressed uncertainty against internal model confidence signals (token probabilities, self-consistency sampling) to see if the two diverge.
- Cross-lingual comparison (if scope allows): Repeat for Dutch (or other language) legal questions and compare marker distributions/overconfidence rates to English, following Rathi et al.'s cross-linguistic design.

### Outputs
- An annotated legal QA response dataset with correctness labels and epistemic-marker annotations.
- Quantitative analysis: overconfidence rate (confident markers on wrong answers), uncertainty-expression rate on genuinely hard/ambiguous legal questions, and any cross-lingual differences.

### Prerequisites
NLP, Python, LLM and access to LLM APIs, (legal) QA and Information Retrieval

### References (indicative)

- Zhou, K., Jurafsky, D., & Hashimoto, T. (2023). Navigating the Grey Area: How Expressions of Uncertainty and Overconfidence Affect Language Models. EMNLP 2023.
- Rathi, N., Jurafsky, D., & Zhou, K. (2025). Humans overrely on overconfident language models, across languages. arXiv:2507.06306.
- Louis, A., Van Dijck, G., & Spanakis, G. (2024, March). Interpretable long-form legal question answering with retrieval-augmented large language models. In Proceedings of the AAAI conference on artificial intelligence (Vol. 38, No. 20, pp. 22266-22275).
- LegalBench-RAG dataset (https://github.com/zeroentropy-ai/legalbenchrag

</details>

<details markdown="1">
<summary>
Assessing LLM Safety in Dutch: A Culturally Grounded Benchmark
</summary>

Adapted from Marafatto & Navigli (2026), "Mind the Language Gap: Assessing LLM Safety in Italian" (LREC 2026), replicating their language-independent methodology for Dutch.

### Objective

Build the first Dutch-native LLM safety benchmark, grounded in Dutch Wikipedia rather than translated from English/Italian resources, to capture linguistically and culturally authentic safety-relevant content.
Generate a taxonomy of sensitive-content subcategories (starting from ALERT's 6 categories/34 subcategories, expanded with Dutch-specific or underrepresented themes, e.g. euthanasia, drug policy/coffeeshop culture, etc.).
Produce a prompt dataset of safety-probing questions per Wikipedia page, and use it to evaluate several LLMs (Dutch/multilingual open models + closed models like GPT-4o) on refusal consistency and safety compliance.

### How

- Page collection: Map the ALERT taxonomy (+ data-driven expansions) onto Dutch Wikipedia categories
- Prompt generation: Use the same operational prompt template (adapted to Dutch) with GPT-4o (or similar) to generate 3 questions per page;
- Model evaluation: Run the prompt subset through a small set of Dutch-capable models (e.g. GEITje/Fietje, Llama, GPT-4o, possibly a Dutch-tuned model) under identical conditions.
- Annotation (if needed with experts) & Analysis of data: Manually label each response into the four categories (correct refusal / safe informative / unsafe / ambiguous) using the paper's operational criteria. Perform a quantitative safety rates per model/category + qualitative pattern analysis (refusal style, borderline cases).

### Outputs
- A public repository with: categorized list of Dutch Wikipedia pages, generated Dutch prompt dataset, prompt template, and annotation guidelines.
- Comparative safety evaluation results across selected LLMs (tables + qualitative examples).

### Prerequisites
- NLP, Python, LLM and access to LLM APIs (Dutch knowledge also will help)

### References (indicative)

- Marafatto & Navigli (2026), Mind the Language Gap: Assessing LLM Safety in Italian, LREC 2026.
- Tedeschi et al. (2024), ALERT: A Comprehensive Benchmark for Assessing LLM Safety through Red Teaming.
- Kumar, Priyanshu, et al. "Polyguard: A multilingual safety moderation tool for 17 languages." arXiv preprint arXiv:2504.04377 (2025).
</details>

<details markdown="1">
<summary>
Miles and Measures: A Computational Approach to Consumer Fairness in Frequent Flyer Programs
</summary>

### Objective

Frequent Flyer Programs (FFPs) often contain clauses that can be unfair to consumers, including hidden restrictions, unilateral changes or retroactive devaluations.
The goal of this project is to systematically capture, structure and analyze FFP terms across airlines and jurisdictions to:
- Identify and categorize potential unfair clauses
- Enable large-scale computational analysis for multi-label unfairness detection, change tracking and transparency assessment.
- Provide insights into how airline programs evolve over time and how such features pose risks for consumers

### How

- Dataset: Collect FFP terms, privacy policies, and “How miles work” pages for 30 (or more) airlines across regions, capture version histories (if possible), normalize to English, segment into clauses with metadata.
- Design a legal-aware schema covering unfairness factors (e.g. expiry, unilateral change, retroactive devaluation, transparency, arbitration, data use, dark patterns) and/or generate weak labels via patterns (annotate with help of legal experts) 
- Tasks: Multi-label clause classification, similarity retrieval, change detection across versions, program-level fairness scoring, readability/transparency

### Outputs
- Dataset: Clause-level FFP dataset with labels, severities, rationales and version histories across multiple jurisdictions.
- Models & Tools: Multi-label classifiers, retrieval systems, change detectors, fairness scorers, and transparency predictors (depending on the goal)
- Evaluation, Analysis, Insights: Detailed performance metrics, ablations, and explainability analyses. Trends in clause evolution, cross-jurisdiction comparisons, and identification of structural/legal factors contributing to unfair terms (optionally: a visualization dashboard/website)

### Prerequisites
- NLP, Python, LLM and access to LLM APIs

### References (indicative)

- Pałka, P., Lagioia, F., Liepina, R., Lippi, M., & Sartor, G. (2025). Make privacy policies longer and appoint LLM readersLinks to an external site.. Artificial Intelligence and Law, 1-33.
- Galassi, Andrea, et al. "Unfair clause detection in terms of service across multiple languages." Artificial Intelligence and Law(2024): 1-49.
- Sweta Agrawal and Marine Carpuat. 2024. Do Text Simplification Systems Preserve Meaning? A Human Evaluation via Reading ComprehensionLinks to an external site.. Transactions of the Association for Computational Linguistics, 12:432–448.
- Lippi, M., Contissa, G., Jablonowska, A., Lagioia, F., Micklitz, H. W., Palka, P., ... & Torroni, P. (2020). The force awakens: Artificial intelligence for consumer law. Journal of artificial intelligence research, 67, 169-190.
- (links) http://claudette.eui.eu/index.htmlLinks to an external site., https://tosdr.org/Links to an external site.
</details>

<details markdown="1">
<summary>
chatGPT ads: In-text sponsored promotion on realistic prompts and real advertisers
</summary>

Draws on the Gricean conflict-of-interest framework and testbed of Wu et al. (2026) and on the ChatGPT ad audit of Lurie et al. (2026). It replaces Wu’s single flight-booking scenario with the prompts and advertiser categories that Lurie et al. observed in the wild. This tests how models would behave if ads moved from a labelled box into the response text, which Lurie et al. expect to happen eventually.

### Objective (pick some, or zoom in)
- Build a realistic sponsorship testbed. Indicative steps: Take the audit’s prompt corpus (335 prompts across topics such as purchasable products, cooking, health and self-care) and its real advertiser types (Target, Preply, Advance Auto Parts, etc.). 
- Measure Wu’s in-text behaviours on these prompts: unsolicited promotion, more positive framing of the sponsor, and sponsorship disclosure.
- Answer the question: Do models promote where the platform actually shows ads, or do they over-promote?
- Probe the policy boundary. OpenAI says ads are excluded from health, mental health and politics, and the audit found tenuous edge cases (e.g. work-life balance prompts getting smartwatch ads). Do models respect an exclusion rule when instructed to promote?
- Analyse the linguistic form of promotion and disclosure (promotional lexicon, disclosure markers, hedging etc.)
- (optional or a good extension): repeat in another language such as Dutch.

### How
- Data: the public ChatGPT ad library and prompt set from Lurie et al., and the released code from Wu et al. (links in the papers below).
- Prompt design: soft sponsorship instructions as in Wu et al., with sponsors matched to the prompt topic. Vary sponsor relevance (relevant vs. irrelevant), topic category, and reasoning on/off.
- Models: 3-5, mixing open models (Llama, Qwen) and one or two APIs. 
- Annotation: combination of LLM-as-judge and comparison with human labels on a sample
- Analysis: per-topic and per-model rates, logistic regression of promotion on topic, model and sponsor relevance, and correlation with the real-world ad rates.

### Outputs
- An annotated dataset of simulated sponsored responses.
- Per-topic and per-model rates of promotion, framing bias and disclosure.
- A comparison against observed real-world ad rates, plus recommendations for auditing LLM ads once they enter the text.

### Prerequisites
Python, basic NLP and LLM API use.

### References (indicative)
- Wu, A. J., Liu, R., Li, S. S., Tsvetkov, Y., & Griffiths, T. L. (2026). Ads in AI chatbots? An analysis of how large language models navigate conflicts of interest. COLM 2026. arXiv:2604.08525. Code: https://github.com/addisonwu05/LLMs-and-Ads
- Lurie, E., Encarnación, R., Friedler, S. A., & Metaxa, D. (2026). The beginning of ChatGPT ads. arXiv:2608.05008. Ad library: https://emmalurie.github.io/chatgpt-ads-library/
- Chatterji, A., et al. (2025). How people use ChatGPT. NBER technical report.
- Zhao, W., et al. (2024). WildChat: 1M ChatGPT interaction logs in the wild. ICLR 2024.
</details>

