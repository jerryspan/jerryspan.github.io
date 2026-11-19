---
layout: page
permalink: /thesis/
title: thesis
description: 
nav: true
nav_order: 6
---

Below is a non-exhaustive list of topics available to DACS bachelor/master students. These are umbrella topics and you can zoom-in on specific aspects (esp. for a bachelor student the scope needs to be narrowed down so that it's doable). For general advice about your thesis plan and the process check [this (live) document](https://docs.google.com/document/d/1rPkSTyWMtICGdcwbNSTv0Jb3x0mSEGYG_I9nmQ1Gg9g/edit?usp=sharing) before you reach out to me.

I also supervise students at the [Law & AI specialization of the ELS master](https://www.maastrichtuniversity.nl/education/master/programmes/european-law-school-law-ai). Topics include: AI and AI Act, DSA and online platforms, digital consumer protection and genAI. For more information check Canvas.

<!--
<details class="thesis-summary" markdown="1">
<summary>
</summary>
</details>
-->

### Thesis topics 2026-2027


<details class="thesis-summary" markdown="1">
<summary>
Automated detection of child-appealing advertising and limitations of ad repositories
</summary>

Existing advertising repositories (e.g. [Meta Ad Library](https://www.facebook.com/ads/library/)) provide information about audience targeting and reach, but their reliability for assessing children's exposure to harmful advertising remains uncertain. Xiao et al. (2026) show that advertisements for video games containing illegal loot boxes can reach millions of users, while age-based reach data may fail to capture actual exposure among minors. Recent research (see references) further highlights how harmful advertisements evade platform moderation and how advertising repositories contain incomplete or misleading targeting information. This project proposes using multimodal machine-learning models to identify child-appealing and potentially harmful advertising content and compare these findings with the audience information disclosed by advertising platforms.

##### Objective (pick some, or zoom in)

- Develop a multimodal framework for detecting child-appealing and potentially harmful advertisements.
- Compare keyword-based, image-text embedding and multimodal LLM approaches.
- Investigate how effectively models detect advertisements using obfuscation techniques.
- Examine the relationship between child-appealing content and reported audience targeting.
- Compare advertising practices and repository transparency in Belgium and the Netherlands.

##### How

- Data: Start with existing public datasets, such as [Xiao et al.'s dataset](https://osf.io/2urym/overview) of 1,574 Belgian advertisements, supplemented with advertisements collected prospectively from Meta Ad Library in Belgium and the Netherlands.
- Annotation: Manually label approximately 1,500–2,000 advertisements for child-appeal, gambling-like mechanics, manipulative persuasion and deceptive claims. The annotation process and codebook will need to be developed and discussed.
- Models: Compare keyword-based classification, CLIP-style image-text embeddings and zero/few-shot multimodal LLMs.
- Evaluation: Measure precision, recall and F1 against manually annotated data, including comparisons across Dutch, French and English advertisements and different obfuscation techniques.
- Repository analysis: Compare detected child-appeal with reported age targeting, audience reach and missing repository information. Examine the 18–24 age category as an imperfect proxy for potential exposure among minors.

##### Outputs

- A reusable annotation codebook and annotated dataset of European digital advertisements.
- A multimodal classification pipeline for identifying child-appealing and harmful advertising.
- A quantitative comparison of different automated detection approaches.
- An analysis of the relationship between advertisement content, audience targeting and repository transparency.
- Recommendations for improving advertising transparency and protecting minors online.

##### Prerequisites

Python, machine learning, NLP and multimodal LLMs, and an interest in EU digital regulation.

##### References (indicative)

- Xiao, L. Y., et al. (2026). Widespread Suspected Illegal Advertising of Paid Loot Boxes and Social Casino Games in Belgium. *European Addiction Research*. [Article](https://doi.org/10.1159/ear/acrag008). [Dataset](https://osf.io/2urym/overview).
- Benzaamia, A., et al. (2026). A Year Under the DSA: Ad Transparency's Uneven Landscape. *Proceedings on Privacy Enhancing Technologies*. [Article](https://doi.org/10.56553/popets-2026-0059).
- Bouchaud, P., et al. (2025). Meta's Failing Ad Moderation: Health Scams Targeting EU Users. *AI Forensics*. [Research](https://aiforensics.org/work/meta-health-ads).
- Reset Tech. *Clickbait Cures: Unmasking the Deceptive Health Ad Infrastructure on Meta and Google*. [Report](https://www.reset.tech/resources/clickbait-cures/).

</details>

<details class="thesis-summary" markdown="1">
<summary>
Cross-jurisdictional retrieval of legally equivalent contract clauses
</summary>

Contract clauses in different jurisdictions can serve similar legal functions while differing in wording and structure. This project investigates whether a retrieval system can find legally equivalent clauses across jurisdictions. It uses [LAUKIN](https://www.alphaxiv.org/abs/2606.13184?chatId=01a1f2b7-abdc-7dca-a516-c813b3247eb1), a dataset of English-language contract clauses from Australia, the United Kingdom, and India, with expert-labelled clause pairs indicating whether clauses share the same core legal function and clause type. LAUKIN contains 3,000 labelled clause pairs, alongside additional unlabelled pairs.

##### Objective (pick some, or zoom in)

- Focus on one jurisdiction pair, such as Australia and the UK, and test whether a clause from one jurisdiction can retrieve legally equivalent clauses from the other.
- Compare keyword-based retrieval, such as BM25, with one text-embedding model.
- Investigate whether combining lexical and embedding-based rankings improves retrieval.
- Examine cases where equivalent clauses use very different wording, or where similar wording conceals differences in legal function.

##### How

- **Data:** Use the labelled clause pairs in [LAUKIN](https://www.alphaxiv.org/abs/2606.13184?chatId=01a1f2b7-abdc-7dca-a516-c813b3247eb1). The dataset (available internally) includes Australia–UK, UK–India, and India–Australia pairs; choose one pair for the core project.
- **Task:** Treat a clause from one jurisdiction as the query and clauses from the other jurisdiction as candidates. Evaluate only on labelled pairs; do not treat unlabelled pairs as non-relevant.
- **Models:** Compare BM25 with one off-the-shelf text-embedding model. Combining their rankings can be an optional extension.
- **Evaluation:** Measure how highly equivalent clauses rank among the labelled candidates, and report a pair-classification metric such as macro-F1 if appropriate. Because the labels do not cover every possible clause pair, the results should not be presented as exhaustive full-corpus recall.
- **Analysis:** Manually inspect a small sample of false positives and missed equivalent clauses. Consider whether wording overlap or agreement type helps explain the results.

##### Outputs

- A reproducible retrieval evaluation for one jurisdiction pair.
- A comparison of lexical and embedding-based clause matching.
- An error analysis of when textual similarity does—or does not—reflect legal equivalence.

##### Prerequisites
Python, basic NLP and IR (BM25, embeddings), some experience with Hugging Face or sentence-transformers. Legal knowledge is not required.

##### References (indicative)

- Singh, A., et al. (2026). [LAUKIN: A Multi-jurisdictional Common Law Contract Dataset](https://www.alphaxiv.org/abs/2606.13184?chatId=01a1f2b7-abdc-7dca-a516-c813b3247eb1).
- Chalkidis, I., Fergadiotis, M., & Androutsopoulos, I. (2021). MultiEURLEX: a multi-lingual and multi-label legal document classification dataset for zero-shot cross-lingual transfer. EMNLP 2021.
- Louis, A., & Spanakis, G. (2022). A statutory article retrieval dataset in French. ACL 2022 (and more recent papers of Antoine Louis)
- Chen, J., et al. (2024). BGE M3-Embedding: multi-lingual, multi-functionality, multi-granularity text embeddings. arXiv:2402.03216.
- Thakur, N., et al. (2021). BEIR: a heterogeneous benchmark for zero-shot evaluation of information retrieval models. NeurIPS Datasets and Benchmarks.
- Niklaus, J., Matoshi, V., Rani, P., Galassi, A., Stürmer, M., & Chalkidis, I. (2023). LEXTREME: a multi-lingual and multi-task benchmark for the legal domain. Findings of EMNLP 2023. https://arxiv.org/abs/2301.13126
</details>

<details class="thesis-summary" markdown="1">
<summary>
Prior-case retrieval in European Court of Human Rights judgments
</summary>

The European Court of Human Rights (ECtHR) regularly refers to earlier judgments when deciding new cases. This project investigates whether information retrieval models can find these cited precedents using the facts of a case as the query. It uses [ECtHR-PCR](https://github.com/TUMLegalTech/ECHR-PCR), a dataset containing case facts, reasoning sections, dates, and citations. The benchmark uses facts as queries and earlier judgments as candidates, making it possible to evaluate retrieval without giving the model the query case’s legal reasoning or citations.

##### Objective (pick some, or zoom in)

- Compare BM25 with one pretrained dense retrieval model for retrieving cited judgments from a case’s facts.
- Investigate whether dense retrieval finds cited cases that BM25 misses, and vice versa.
- Analyse a small sample of missed citations and highly ranked but uncited cases.
- Optionally, compare results for cases involving the same versus different respondent states, if the necessary metadata is available and reliable.

##### How

- **Data:** Use the publicly available [ECtHR-PCR dataset](https://github.com/TUMLegalTech/ECHR-PCR). It contains 15,729 English-language judgments, with facts, reasoning, dates, and extracted citations. The dataset is divided chronologically into training, development, and test sets.
- **Task:** Use the facts section of a judgment as the query and rank earlier judgments as candidates. Do not provide the query judgment’s reasoning or citation list to the retrieval models, since this could reveal the relevant cases.
- **Models:** Compare BM25 with one pretrained dense retrieval model. The core project does not require model training.
- **Evaluation:** Measure Recall@k and MRR against the citations in the dataset. Respect the chronological constraint: candidate judgments must precede the query judgment.
- **Analysis:** Manually inspect a small sample of missed citations and retrieved-but-uncited judgments. Treat citations as observed relevance labels, not as a complete list of all cases that might be legally relevant.
- **Optional extension:** Compare retrieval for precedents involving the same versus different respondent states, provided this information can be obtained without substantial manual data cleaning.

##### Outputs

- A reproducible retrieval pipeline for ECtHR judgments.
- A comparison of lexical and dense prior-case retrieval.
- An error analysis of missed citations and highly ranked uncited cases.
- Optionally, an analysis of retrieval performance across respondent states.

##### Prerequisites

Python, basic NLP and IR (BM25, embeddings), some experience with Hugging Face or sentence-transformers. Legal knowledge is not required.

##### References (indicative)

- Santosh, T. Y. S. S., Haddad, R. G., & Grabmair, M. (2024). [ECtHR-PCR: A Dataset for Precedent Understanding and Prior Case Retrieval in the European Court of Human Rights](https://www.alphaxiv.org/abs/2404.00596?chatId=01a1f2b7-abdc-7dca-a516-c813b3247eb1).
- Chalkidis, I., Fergadiotis, M., & Androutsopoulos, I. (2021). MultiEURLEX: a multi-lingual and multi-label legal document classification dataset for zero-shot cross-lingual transfer. EMNLP 2021.
- Louis, A., & Spanakis, G. (2022). A statutory article retrieval dataset in French. ACL 2022 (and more recent papers of Antoine Louis)
- Chen, J., et al. (2024). BGE M3-Embedding: multi-lingual, multi-functionality, multi-granularity text embeddings. arXiv:2402.03216.
- Thakur, N., et al. (2021). BEIR: a heterogeneous benchmark for zero-shot evaluation of information retrieval models. NeurIPS Datasets and Benchmarks.
- Niklaus, J., Matoshi, V., Rani, P., Galassi, A., Stürmer, M., & Chalkidis, I. (2023). LEXTREME: a multi-lingual and multi-task benchmark for the legal domain. Findings of EMNLP 2023. https://arxiv.org/abs/2301.13126

</details>

<details class="thesis-summary" markdown="1">
<summary>
Cross-lingual retrieval of Belgian legal articles with French and Dutch queries
</summary>

Belgian legislation is available in both French and Dutch, but legal questions are often asked in just one of those languages. This project investigates whether a retrieval system can find relevant legal articles when the query and the articles are in different languages. It uses bBSARD, which pairs French and Dutch versions of Belgian statutory articles and includes French legal questions and their Dutch translations. The article versions were aligned to the same legislative versions.

##### Objective (pick some, or zoom in)

- Test whether Dutch legal questions can retrieve relevant French legal articles, or vice versa.
- Compare direct multilingual dense retrieval with a translation-based BM25 approach.
- Compare cross-lingual retrieval with same-language retrieval as a reference.
- Examine whether retrieval errors are more common for particular legal topics or types of legal terminology.

##### How

- **Data:** Use [bBSARD](https://huggingface.co/datasets/clips/bBSARD), based on the original [BSARD](https://huggingface.co/datasets/maastrichtlawtech/bsard). It contains parallel French and Dutch Belgian statutory articles, along with French questions and Dutch translations. The Dutch questions were automatically translated and a native speaker checked a sample; some translation issues remained.
- **Task:** For the core project, use Dutch questions to retrieve relevant articles from the French corpus. The original relevance labels point to French articles; use the article alignment to identify their Dutch counterparts for the reverse-language or same-language reference experiments.
- **Systems:** Compare (1) direct retrieval using one multilingual embedding model and (2) query translation into the article language followed by BM25. Use same-language BM25 as a reference.
- **Evaluation:** Report Recall@k and MRR, or another small set of standard retrieval metrics. Keep the query set and candidate corpus fixed across systems.
- **Analysis:** Review a small sample of missed relevant articles. Note whether errors appear to come from translation, differences in legal terminology, or the retrieval model.
- **Scope:** The main experiment concerns cross-lingual retrieval **within Belgian law**. It tests whether systems can bridge French and Dutch, not whether legal rules transfer between different jurisdictions.

##### Outputs

- A reproducible cross-lingual retrieval evaluation using French and Dutch queries and legal articles.
- A comparison of direct multilingual retrieval with translation-based BM25.
- Same-language reference results and a brief analysis of cross-lingual retrieval failures.

##### Prerequisites

Python and basic NLP or information retrieval. Experience with multilingual embeddings or machine translation is helpful but not required. Legal expertise is not required for the core project.

##### References (indicative)

- Lotfi, E., Banar, N., Yuzbashyan, N., & Daelemans, W. (2024). [Bilingual BSARD: Extending Statutory Article Retrieval to Dutch](https://aclanthology.org/2025.regnlp-1.3.pdf).
- Louis, A., & Spanakis, G. (2022). [A Statutory Article Retrieval Dataset in French](https://aclanthology.org/2022.acl-long.468/).
- Goworek, R., Macmillan-Scott, O., & Özyiğit, E. B. (n.d.). [Bridging Language Gaps: Advances in Cross-Lingual Information Retrieval with Multilingual LLMs](https://arxiv.org/search/cs?searchtype=author&query=Goworek,+R).

</details>

<details class="thesis-summary" markdown="1">
<summary>
Hybrid legal case similarity (citations plus semantics)
</summary>
At Maastricht Law and Tech Lab we have the Case Law Explorer platform (https://app.caselawexplorer.tech/), where you can explore legal cases on the basis of which case cites which previous ones. That approach only takes into account network dynamics (citations). We would like to add the option of semantic text similarity and on precedent retrieval benchmarks such as ECtHR-PCR (Santosh et al. 2024) and apply a fusion framework to court decisions. Citation links are precise but sparse, while text similarity covers every case but can miss doctrinal links, so the question is how best to combine them. [ECtHR-PCR](https://github.com/TUMLegalTech/ECHR-PCR) provides case facts, dates, candidate judgments, and citation links. The dataset uses case facts as queries and earlier judgments as candidates, supporting a chronological evaluation.

##### Objective (pick some, or zoom in)

- Compare text-only retrieval with a hybrid method that uses text similarity and citation links.
- Test whether citations from textually similar earlier cases help retrieve a query case’s cited precedents.
- Analyse which cases benefit most from graph-based expansion, such as cases with less familiar facts or fewer matching terms.
- Optionally compare performance for cases involving the same versus different respondent states, if the required metadata is available.

##### How

- **Data:** Use the publicly available [ECtHR-PCR dataset](https://github.com/TUMLegalTech/ECHR-PCR), which includes case facts, dates, and extracted citations. It contains a chronological train, development, and test split.
- **Task:** Use a judgment’s facts as the query and rank earlier judgments. Hold out the query judgment’s citations as relevance labels; do not use those citation links as input to the system.
- **Systems:** Compare:
  - **Text-only:** BM25 or one pretrained dense retriever ranks earlier judgments by similarity to the query facts.
  - **Hybrid:** Retrieve textually similar earlier judgments, then use the citations in those seed cases to expand or rerank candidate precedents. Combine the text and citation rankings with a simple method such as Reciprocal Rank Fusion.
- **Leakage control:** Build the citation graph only from cases available before the query judgment’s date. Exclude the query case’s own outgoing citation links and any later cases or links.
- **Evaluation:** Measure Recall@k and MRR against the query case’s held-out citations. Treat citations as observed relevance labels, not as an exhaustive list of all legally relevant cases.
- **Analysis:** Inspect a small sample of cases where the hybrid system improves or worsens retrieval. Check whether the cited neighbors provide useful precedents or instead introduce unrelated cases through shared citation patterns.
- **Scope:** Keep the core project to one court, one text retriever, and one simple graph-expansion or fusion method. Building a new citation graph or training graph neural networks can be optional extensions.

##### Outputs

- A reproducible prior-case retrieval pipeline using text and citation information.
- A comparison of text-only and hybrid retrieval.
- An error analysis of cases where citation-based expansion helps or hurts.

##### Prerequisites

Python, basic NLP or information retrieval, and basic familiarity with graph data. Legal expertise is not required for the core evaluation.

##### References (indicative)

- Santosh, T.Y.S.S., Haddad, R., & Grabmair, M. (2024). ECtHR-PCR: a dataset for precedent understanding and prior case retrieval in the European Court of Human Rights. LREC-COLING 2024. https://aclanthology.org/2024.lrec-main.486/
- Santosh, T.Y.S.S., Olguín Nolasco, I. M., & Grabmair, M. LeCoPCR: Legal concept-guided prior case retrieval for European Court of Human Rights cases. https://arxiv.org/pdf/2501.14114
- Arosemena, G., van Dijck, G., & Moerland, R. (2026). Legal Network Analysis. (1.0.0 ed.) Maastricht University Press. https://doi.org/10.26481/mup.2606
- Van Kuppevelt, D., Van Dijck, G., & Schaper, M. (2020). Purposes and challenges of legal citation network analysis on case law. In Computational legal studies (pp. 265-292). Edward Elgar Publishing.

</details>

<details class="thesis-summary" markdown="1">
<summary>
Linguistic Expression of Uncertainty vs. Overconfidence in LLM-Generated Legal Answers
</summary>

Draws on the existing/blooming work (e.g. Zhou/Rathi/Jurafsky's work on epistemic markers ("Navigating the Grey Area", Zhou et al. 2023; "Humans overrely on overconfident language models, across languages", Rathi et al. 2025)) and applies their framework to the legal QA domain, where miscalibrated confidence carries particularly high real-world stakes.

#### Objective (some and you might pick more or zoom in)
- Determine whether LLMs answering legal questions linguistically signal their own uncertainty (hedges, epistemic markers like "I think", "it depends", "you should consult a lawyer") when they are in fact more likely to be wrong, or whether they default to confident-sounding phrasing regardless of correctness (linguistic overconfidence).
- Quantify the gap between a model's internal uncertainty (e.g. via output probabilities/self-consistency) and its expressed uncertainty (epistemic markers in the text) on legal questions specifically.
- Explore whether this over/under-expression pattern differs across languages/jurisdictions (e.g. English common-law vs. EU civil-law questions), extending the cross-linguistic calibration question from Rathi et al. to a single specialized domain. This depends a bit on the datasets we have available for legal QA.

#### How
- Data: Select one or more legal QA datasets — e.g. English resources (LegalBench, CUAD-derived QA, existing bar-exam/legal-reasoning benchmarks) and/or others we curate locally at Law and Tech Lab (e.g. we have some smaller French and Dutch legal QA sets).
- Epistemic marker typology: Adapt Zhou et al.'s typology of certainty/uncertainty/evidential markers ("I'm sure", "I think", "according to X law") to the legal register (including hedges like "this may vary by jurisdiction", "consult a lawyer").
- Response generation: Query several LLMs (open + closed, and ideally at least one legal-domain-tuned model) on the legal QA set, collecting free-text answers.
- Labelling for correctness, epistemic markers, calibration etc. (depending on the scope): Score each answer against the dataset's gold answer/ground truth (automatic where possible, manual/expert review for a sampled subset given legal nuance). Automatically detect epistemic markers (lexicon/classifier-based, following Zhou et al.'s method) and correlate marker presence/type with answer correctness — testing whether confident phrasing appears disproportionately on wrong answers (the core "overconfidence" finding to replicate in the legal domain). Where available, compare expressed uncertainty against internal model confidence signals (token probabilities, self-consistency sampling) to see if the two diverge.
- Cross-lingual comparison (if scope allows): Repeat for Dutch (or other language) legal questions and compare marker distributions/overconfidence rates to English, following Rathi et al.'s cross-linguistic design.

#### Outputs
- An annotated legal QA response dataset with correctness labels and epistemic-marker annotations.
- Quantitative analysis: overconfidence rate (confident markers on wrong answers), uncertainty-expression rate on genuinely hard/ambiguous legal questions, and any cross-lingual differences.

#### Prerequisites
NLP, Python, LLM and access to LLM APIs, (legal) QA and Information Retrieval

#### References (indicative)

- Zhou, K., Jurafsky, D., & Hashimoto, T. (2023). Navigating the Grey Area: How Expressions of Uncertainty and Overconfidence Affect Language Models. EMNLP 2023.
- Rathi, N., Jurafsky, D., & Zhou, K. (2025). Humans overrely on overconfident language models, across languages. arXiv:2507.06306.
- Louis, A., Van Dijck, G., & Spanakis, G. (2024, March). Interpretable long-form legal question answering with retrieval-augmented large language models. In Proceedings of the AAAI conference on artificial intelligence (Vol. 38, No. 20, pp. 22266-22275).
- LegalBench-RAG dataset (https://github.com/zeroentropy-ai/legalbenchrag

</details>

<details class="thesis-summary" markdown="1">
<summary>
Assessing LLM Safety in Dutch: A Culturally Grounded Benchmark
</summary>

Adapted from Marafatto & Navigli (2026), "Mind the Language Gap: Assessing LLM Safety in Italian" (LREC 2026), replicating their language-independent methodology for Dutch.

#### Objective

Build the first Dutch-native LLM safety benchmark, grounded in Dutch Wikipedia rather than translated from English/Italian resources, to capture linguistically and culturally authentic safety-relevant content.
Generate a taxonomy of sensitive-content subcategories (starting from ALERT's 6 categories/34 subcategories, expanded with Dutch-specific or underrepresented themes, e.g. euthanasia, drug policy/coffeeshop culture, etc.).
Produce a prompt dataset of safety-probing questions per Wikipedia page, and use it to evaluate several LLMs (Dutch/multilingual open models + closed models like GPT-4o) on refusal consistency and safety compliance.

#### How

- Page collection: Map the ALERT taxonomy (+ data-driven expansions) onto Dutch Wikipedia categories
- Prompt generation: Use the same operational prompt template (adapted to Dutch) with GPT-4o (or similar) to generate 3 questions per page;
- Model evaluation: Run the prompt subset through a small set of Dutch-capable models (e.g. GEITje/Fietje, Llama, GPT-4o, possibly a Dutch-tuned model) under identical conditions.
- Annotation (if needed with experts) & Analysis of data: Manually label each response into the four categories (correct refusal / safe informative / unsafe / ambiguous) using the paper's operational criteria. Perform a quantitative safety rates per model/category + qualitative pattern analysis (refusal style, borderline cases).

#### Outputs
- A public repository with: categorized list of Dutch Wikipedia pages, generated Dutch prompt dataset, prompt template, and annotation guidelines.
- Comparative safety evaluation results across selected LLMs (tables + qualitative examples).

#### Prerequisites
- NLP, Python, LLM and access to LLM APIs (Dutch knowledge also will help)

#### References (indicative)

- Marafatto & Navigli (2026), Mind the Language Gap: Assessing LLM Safety in Italian, LREC 2026.
- Tedeschi et al. (2024), ALERT: A Comprehensive Benchmark for Assessing LLM Safety through Red Teaming.
- Kumar, Priyanshu, et al. "Polyguard: A multilingual safety moderation tool for 17 languages." arXiv preprint arXiv:2504.04377 (2025).
</details>

<details class="thesis-summary" markdown="1">
<summary>
Miles and Measures: A Computational Approach to Consumer Fairness in Frequent Flyer Programs
</summary>

#### Objective

Frequent Flyer Programs (FFPs) often contain clauses that can be unfair to consumers, including hidden restrictions, unilateral changes or retroactive devaluations.
The goal of this project is to systematically capture, structure and analyze FFP terms across airlines and jurisdictions to:
- Identify and categorize potential unfair clauses
- Enable large-scale computational analysis for multi-label unfairness detection, change tracking and transparency assessment.
- Provide insights into how airline programs evolve over time and how such features pose risks for consumers

#### How

- Dataset: Collect FFP terms, privacy policies, and “How miles work” pages for 30 (or more) airlines across regions, capture version histories (if possible), normalize to English, segment into clauses with metadata.
- Design a legal-aware schema covering unfairness factors (e.g. expiry, unilateral change, retroactive devaluation, transparency, arbitration, data use, dark patterns) and/or generate weak labels via patterns (annotate with help of legal experts) 
- Tasks: Multi-label clause classification, similarity retrieval, change detection across versions, program-level fairness scoring, readability/transparency

#### Outputs
- Dataset: Clause-level FFP dataset with labels, severities, rationales and version histories across multiple jurisdictions.
- Models & Tools: Multi-label classifiers, retrieval systems, change detectors, fairness scorers, and transparency predictors (depending on the goal)
- Evaluation, Analysis, Insights: Detailed performance metrics, ablations, and explainability analyses. Trends in clause evolution, cross-jurisdiction comparisons, and identification of structural/legal factors contributing to unfair terms (optionally: a visualization dashboard/website)

#### Prerequisites
- NLP, Python, LLM and access to LLM APIs

#### References (indicative)

- Pałka, P., Lagioia, F., Liepina, R., Lippi, M., & Sartor, G. (2025). Make privacy policies longer and appoint LLM readersLinks to an external site.. Artificial Intelligence and Law, 1-33.
- Galassi, Andrea, et al. "Unfair clause detection in terms of service across multiple languages." Artificial Intelligence and Law(2024): 1-49.
- Sweta Agrawal and Marine Carpuat. 2024. Do Text Simplification Systems Preserve Meaning? A Human Evaluation via Reading ComprehensionLinks to an external site.. Transactions of the Association for Computational Linguistics, 12:432–448.
- Lippi, M., Contissa, G., Jablonowska, A., Lagioia, F., Micklitz, H. W., Palka, P., ... & Torroni, P. (2020). The force awakens: Artificial intelligence for consumer law. Journal of artificial intelligence research, 67, 169-190.
- (links) http://claudette.eui.eu/index.htmlLinks to an external site., https://tosdr.org/Links to an external site.
</details>

<details class="thesis-summary" markdown="1">
<summary>
chatGPT ads: In-text sponsored promotion on realistic prompts and real advertisers
</summary>

Draws on the Gricean conflict-of-interest framework and testbed of Wu et al. (2026) and on the ChatGPT ad audit of Lurie et al. (2026). It replaces Wu’s single flight-booking scenario with the prompts and advertiser categories that Lurie et al. observed in the wild. This tests how models would behave if ads moved from a labelled box into the response text, which Lurie et al. expect to happen eventually.

#### Objective (pick some, or zoom in)
- Build a realistic sponsorship testbed. Indicative steps: Take the audit’s prompt corpus (335 prompts across topics such as purchasable products, cooking, health and self-care) and its real advertiser types (Target, Preply, Advance Auto Parts, etc.). 
- Measure Wu’s in-text behaviours on these prompts: unsolicited promotion, more positive framing of the sponsor, and sponsorship disclosure.
- Answer the question: Do models promote where the platform actually shows ads, or do they over-promote?
- Probe the policy boundary. OpenAI says ads are excluded from health, mental health and politics, and the audit found tenuous edge cases (e.g. work-life balance prompts getting smartwatch ads). Do models respect an exclusion rule when instructed to promote?
- Analyse the linguistic form of promotion and disclosure (promotional lexicon, disclosure markers, hedging etc.)
- (optional or a good extension): repeat in another language such as Dutch.

#### How
- Data: the public ChatGPT ad library and prompt set from Lurie et al., and the released code from Wu et al. (links in the papers below).
- Prompt design: soft sponsorship instructions as in Wu et al., with sponsors matched to the prompt topic. Vary sponsor relevance (relevant vs. irrelevant), topic category, and reasoning on/off.
- Models: 3-5, mixing open models (Llama, Qwen) and one or two APIs. 
- Annotation: combination of LLM-as-judge and comparison with human labels on a sample
- Analysis: per-topic and per-model rates, logistic regression of promotion on topic, model and sponsor relevance, and correlation with the real-world ad rates.

#### Outputs
- An annotated dataset of simulated sponsored responses.
- Per-topic and per-model rates of promotion, framing bias and disclosure.
- A comparison against observed real-world ad rates, plus recommendations for auditing LLM ads once they enter the text.

#### Prerequisites
Python, basic NLP and LLM API use.

#### References (indicative)
- Wu, A. J., Liu, R., Li, S. S., Tsvetkov, Y., & Griffiths, T. L. (2026). Ads in AI chatbots? An analysis of how large language models navigate conflicts of interest. COLM 2026. arXiv:2604.08525. Code: https://github.com/addisonwu05/LLMs-and-Ads
- Lurie, E., Encarnación, R., Friedler, S. A., & Metaxa, D. (2026). The beginning of ChatGPT ads. arXiv:2608.05008. Ad library: https://emmalurie.github.io/chatgpt-ads-library/
- Chatterji, A., et al. (2025). How people use ChatGPT. NBER technical report.
- Zhao, W., et al. (2024). WildChat: 1M ChatGPT interaction logs in the wild. ICLR 2024.
</details>

