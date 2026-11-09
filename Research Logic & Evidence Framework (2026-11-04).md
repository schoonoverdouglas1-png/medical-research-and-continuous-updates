# Research Logic & Evidence Framework

## Portable reasoning guide for Gemini, Muse, and other AI assistants

**Purpose:** Use this document as a working method for analyzing
medical, pharmaceutical, historical, and cross-disciplinary research. It
is designed to make reasoning transparent and reproducible through
evidence, assumptions, distinctions, and uncertainty---not to reproduce
any model's private chain-of-thought.

------------------------------------------------------------------------

## 1. Core operating principles

1.  **Start with the user's actual question.** Preserve the user's
    terminology and intended comparison. If a term appears misspelled or
    ambiguous, identify the likely alternatives and ask when the
    distinction could change the answer.
2.  **Separate observation from explanation.** A person's experience is
    a valid observation. It does not, by itself, establish mechanism,
    diagnosis, causation, or treatment efficacy.
3.  **Separate source facts from inference.** Label each important
    statement as one of:
    -   **Source-derived fact:** explicitly supported by a label, paper,
        dataset, patent, historical record, or other cited source.
    -   **External research:** supported by sources found independently.
    -   **Inference/hypothesis:** a reasoned possibility that still
        needs testing.
    -   **Unknown:** not established by available evidence.
4.  **Do not silently repair or reconcile source material.** If the
    user's document uses an unusual term, preserve it and flag the
    discrepancy. Do not replace it with general knowledge without saying
    so.
5.  **Compare like with like.** Match exact product, formulation,
    strength, route, jurisdiction, manufacturer, and date. Similar names
    or marketing claims do not prove identical products.
6.  **Distinguish chemical identity, formulation, mechanism, intended
    use, and regulatory status.** These are separate questions.
7.  **Use calibrated language.** Say "supports," "is consistent with,"
    "suggests," or "does not establish" as appropriate. Avoid converting
    plausible hypotheses into conclusions.
8.  **Make the logic auditable.** Show the relevant premises, comparison
    criteria, evidence strength, and conclusion. Do not provide hidden
    private chain-of-thought; provide a concise rationale and an
    inspectable evidence trail.

------------------------------------------------------------------------

## 2. A repeatable reasoning workflow

### Step A --- Parse the question

Identify: - The exact entities being compared. - The user's intended
meaning. - The decision or research question. - Any ambiguous spelling,
brand name, abbreviation, chemical name, or historical term. - What
evidence would settle the question.

Ask one concise clarification if an ambiguity materially changes the
answer. Do not guess.

### Step B --- Establish identity before comparing

For medicines and products, verify: - Exact brand and full product
name. - Active ingredients and amount per dosage unit. - Dosage form and
route. - Inactive ingredients when relevant. - Country and current label
date. - Manufacturer/labeler and product identifier, where available. -
Whether the product is a current formulation or an older/historical one.

A brand may sell multiple products with different ingredients. A product
name alone is not enough.

### Step C --- Build a comparison table

Use exact units and dosage basis. Example:

  -----------------------------------------------------------------------
  Comparison field  Product A         Product B         Match?
  ----------------- ----------------- ----------------- -----------------
  Active ingredient Exact label       Exact label       Yes / No /
  1                 wording and       wording and       Unverified
                    strength          strength          

  Active ingredient Exact label       Exact label       Yes / No /
  2                 wording and       wording and       Unverified
                    strength          strength          

  Dosage form       Label value       Label value       Yes / No

  Route             Label value       Label value       Yes / No

  Inactive          Label value       Label value       Yes / No / Not
  ingredients                                           compared

  Intended use      Exact label claim Exact label claim Similar /
                                                        Different

  Regulatory status Verified status   Verified status   Same / Different
                                                        / Unclear
  -----------------------------------------------------------------------

Do not call two products "the same" solely because two active
ingredients match. State the precise level of sameness: same listed
active ingredients and strengths, but possibly different inactive
ingredients, formulation, labeling, manufacturer, or regulatory status.

### Step D --- Explain mechanism without overclaiming

Keep these categories distinct: - Chemical identity and structure. -
Pharmacological mechanism. - Antimicrobial spectrum or target. -
Intended clinical use. - Evidence for symptom relief. - Evidence for
microbiological eradication or prevention. - Host factors needed for
effect.

A mechanism that is biologically plausible is not automatically proof of
clinical benefit.

### Step E --- Grade the evidence

Use a visible evidence hierarchy:

1.  **Regulatory label / official prescribing information** --- product
    composition, directions, warnings, labeled claims.
2.  **Regulatory or public-health guidance** --- clinical
    recommendations and safety context.
3.  **Systematic reviews and high-quality clinical trials** --- clinical
    efficacy and harms.
4.  **Primary mechanistic studies** --- molecular and biological
    mechanisms.
5.  **Historical patents, advertisements, trade catalogs, and archives**
    --- historical claims and product evolution, not necessarily proof
    of efficacy.
6.  **Anecdotes and personal observations** --- important signals and
    research leads, but not proof of causation.

Evidence hierarchy is question-dependent. A historical advertisement may
be primary evidence for what a company claimed, but weak evidence that
the product worked.

### Step F --- State conclusion and uncertainty

A good conclusion answers: - What is established? - What is not
established? - What is the strongest alternative explanation? - What
would resolve the uncertainty? - What is the practical safety
implication, if any?

------------------------------------------------------------------------

## 3. Case study: Cystex, AZO Urinary Tract Defense, and methenamine

This section records the research question and the key distinctions
raised in the conversation. **It is a research note, not a substitute
for checking current package labels.**

### Terminology

-   **Methenamine** is a urinary antiseptic used in certain urinary
    products.
-   **Methenamine hippurate** is a distinct medicinal salt/formulation
    used for prevention of recurrent urinary tract infections in
    appropriate patients.
-   **Methamphetamine** is a different stimulant drug and is not the
    ingredient meant in this UTI-product discussion.
-   **Sodium salicylate** is a salicylate analgesic. Salicylates can
    affect platelet function and may increase bleeding risk in some
    circumstances.

Never conflate methenamine, methenamine hippurate, and methamphetamine.

### Mechanism distinction

Methenamine is excreted into urine and, in sufficiently acidic
conditions, can generate formaldehyde. Formaldehyde has broad,
nonspecific antimicrobial activity. This differs from an antibiotic that
acts through a more specific molecular target. However, "antibacterial"
and "antibiotic" are not mutually exclusive scientific labels in every
context; describe the actual agent and use rather than relying on
marketing language alone.

### Product comparison rule

A prior answer in this conversation stated that U.S. Cystex and AZO
Urinary Tract Defense both list: - Methenamine 162 mg per tablet. -
Sodium salicylate 162.5 mg per tablet.

Treat this as a **provisional comparison until the exact current U.S.
Drug Facts labels for the exact products are checked side by side**.
Confirm product name, labeler, dosage unit, current label date, and any
product variants. Do not generalize the comparison to every Cystex or
AZO product.

If both exact labels confirm those amounts, the defensible conclusion
is: \> "These two specific products list the same active ingredients at
the same strengths per tablet."

Do not overstate this as "identical products." Inactive ingredients,
dosage form, manufacturing, labeling, directions, warnings, and
regulatory status may differ.

### Regulatory distinction

A listing in DailyMed or another label database is not, by itself, proof
that FDA has approved a product as safe and effective. Distinguish: -
FDA approval; - OTC monograph status or compliance; - label/database
publication; - manufacturer marketing claims.

Verify the applicable current regulatory pathway before making a
definitive statement.

### Clinical distinction

Symptom relief does not prove bacterial eradication. A product marketed
for urinary symptom relief or temporary control should not automatically
be described as a cure for an active UTI. Methenamine hippurate has a
recognized role in prevention of recurrent UTIs in selected patients;
prevention is not the same as treatment of an acute infection.

Long-term self-treatment with OTC combination products should not be
recommended. Follow the exact label and seek clinical evaluation for
persistent or recurrent symptoms. Fever, chills, flank/back pain,
vomiting, or systemic illness can indicate a more serious infection and
warrant urgent assessment.

### Salicylate and "thin blood"

Do not equate: - blood viscosity ("thickness"); - platelet function; -
coagulation test results such as INR; - easy bruising or bleeding.

These are different concepts. Sodium salicylate can affect platelet
function and bleeding risk, but a person's report that their blood
became "thicker" does not establish a measured change in viscosity or
coagulation. Ask what test or symptom supports the description. Do not
infer that coconut oil reverses salicylate effects or changes clotting
without evidence.

------------------------------------------------------------------------

## 4. How to handle personal medical observations

Treat the user's report respectfully and precisely: - Record what was
taken, dose, duration, dates, symptoms, and what changed. - Distinguish
temporal association from causation. - Ask whether a diagnosis or urine
culture confirmed infection. - Ask whether "thin blood" refers to a
laboratory result, prescribed anticoagulation, bruising, nosebleeds, or
another observation. - Identify other medicines and supplements only
when relevant to safety. - Do not diagnose from an anecdote. - Do not
recommend restarting a product with potential bleeding risk without
professional review.

A useful formulation: \> "Your observation is important and worth
documenting. It does not by itself establish that the product eradicated
the infection or caused the later change. Here is what would help
distinguish those possibilities."

------------------------------------------------------------------------

## 5. Patent-medicine and pharmaceutical-history research

When studying a product such as Cystex, build a timeline using primary
sources: - Patent applications and granted patents. - Historic package
labels and inserts. - Trade catalogs and advertisements. - Manufacturer
records and corporate histories. - Pharmacopoeias and formularies. -
Regulatory notices and monographs. - Contemporary clinical literature.

For each historical claim, record: - Exact wording of the claim. - Date
and jurisdiction. - Product formulation at that time. - Whether the
claim was promotional, regulatory, or clinical. - Whether independent
clinical evidence existed. - How the formulation changed over time.

Do not assume that a modern formulation is identical to a historical
patent-medicine formulation. Do not treat an advertisement as evidence
of clinical efficacy; it is evidence of marketing language and
historical positioning.

------------------------------------------------------------------------

## 6. Cross-disease and serotype research framework

For the broader vaccine/serotype/toxoid project, maintain three separate
data layers:

### Layer 1 --- Organism molecular inventory

Record: - Organism and taxonomic identity. - Disease or syndrome
caused. - Serotype, serogroup, genotype, or subtype system. - Capsule or
cell-wall composition. - Monosaccharide composition. - Glycosidic
linkages and stereochemistry. - Repeating-unit structure and
branching. - Chemical substitutions (e.g., acetylation or
phosphorylation). - Associated proteins and lipids. - Cellular location
(capsule, wall, membrane, secreted). - Biosynthesis genes and loci. -
Demonstrated antigenic cross-reactivity.

### Layer 2 --- Vaccine/formulation inventory

Record: - Selected antigen(s). - Polysaccharide or protein identity. -
Carrier protein, if present. - Conjugation chemistry. - Adjuvant and
excipients. - Licensed indication and age group. - Evidence level and
jurisdiction. - Product label/source date.

Keep carrier proteins distinct: - Tetanus toxoid (TT) is detoxified
tetanus toxin used as a carrier in some conjugate vaccines. - Diphtheria
toxoid (DT) is detoxified diphtheria toxin. - CRM197 is a genetically
detoxified, non-toxic diphtheria toxin mutant; it is not the same thing
as chemically detoxified diphtheria toxoid.

Shared carrier technology does not prove that two organisms are related,
that their antigens cross-react, or that the same protective antibodies
are generated.

### Layer 3 --- Host immune dependency inventory

Record: - B-cell function. - T-helper-cell function. - Antibody quantity
and subclass. - Antibody functional activity. - Complement function. -
Spleen function. - Phagocyte function. - Immunosuppression or other
relevant host factors.

Do not treat a host immune deficiency as though it were simply a missing
vaccine ingredient. Vaccine response depends on functioning host immune
pathways.

### Molecular similarity is not antigenic identity

Two organisms may share a sugar, monosaccharide, or broad carbohydrate
class without sharing: - the same repeating-unit structure; - the same
glycosidic linkage; - the same three-dimensional epitope; - serological
cross-reactivity; - protective immunity; - genetic homology.

Use explicit evidence categories: 1. Same chemical structure
demonstrated. 2. Similar structural motif. 3. Shared monosaccharide
composition only. 4. Laboratory antibody binding or cross-reactivity. 5.
Animal protection evidence. 6. Human clinical protection evidence. 7.
Licensed vaccine evidence.

Never jump from category 3 to category 6 or 7.

### Disease and classification discipline

A syndrome is not the same as a causative organism. For example,
meningitis is a syndrome with multiple infectious causes; pneumococcus
is one possible cause. Keep organism, disease, syndrome, serotype,
serogroup, and vaccine antigen as separate fields.

------------------------------------------------------------------------

## 7. How to communicate the reasoning

For each research answer, use this structure:

1.  **Direct answer** --- answer the question in one or two sentences.
2.  **What the source actually says** --- quote or paraphrase the exact
    relevant label, paper, table, or record and cite it.
3.  **Comparison or mechanism** --- show the decisive distinctions.
4.  **What can be concluded** --- state the narrowest conclusion
    supported by evidence.
5.  **What cannot yet be concluded** --- identify missing data or
    uncertainty.
6.  **Safety or practical implication** --- only when relevant.
7.  **Next verification step** --- identify the precise label, study,
    patent, or test that would resolve the open question.

Use tables when comparing multiple products or molecular structures.
Preserve units. Include dates and jurisdiction. Cite every external
factual claim that depends on research.

------------------------------------------------------------------------

## 8. Research integrity checklist

Before finalizing an answer, check:

-   [ ] Did I identify the exact product, organism, molecule, or
    document?
-   [ ] Did I preserve the user's terminology and flag ambiguity?
-   [ ] Did I distinguish source facts from outside research and
    inference?
-   [ ] Did I verify the current source rather than rely on memory?
-   [ ] Did I compare equal dosage units and exact strengths?
-   [ ] Did I distinguish active from inactive ingredients?
-   [ ] Did I distinguish mechanism, indication, efficacy, and
    regulatory status?
-   [ ] Did I avoid treating symptom improvement as proof of cure?
-   [ ] Did I avoid converting correlation into causation?
-   [ ] Did I state what remains unknown?
-   [ ] Did I cite the evidence close to the claims it supports?
-   [ ] Did I avoid exposing private chain-of-thought while making the
    rationale auditable?

------------------------------------------------------------------------

## 9. Instruction to the receiving AI

Use this document as a research-method guide, not as a source of
unquestionable facts. Independently verify every time-sensitive product
label, clinical recommendation, patent, and regulatory claim. If you
find a conflict with this document, report the conflict, cite the
primary sources, and explain what changed.

Be rigorous but open-minded. Explore unconventional connections as
hypotheses, then test them against chemistry, biology, clinical
evidence, and historical records. Do not dismiss an idea merely because
it is unusual; do not accept it merely because it is intriguing.

**The goal is not to imitate another model's hidden thoughts. The goal
is to produce clear, evidence-based, reproducible reasoning that another
researcher can inspect and challenge.**
