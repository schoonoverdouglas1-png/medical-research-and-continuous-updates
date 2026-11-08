# Mayo Clinic Encephalitis / Meningitis PCR Panels — Research Report

## Summary

**Headline answer — read this first, because it overturns the premise of a "blood encephalitis PCR panel":**

Mayo Clinic Laboratories (MCL) does **not** offer a multiplex blood (serum/plasma/whole-blood) version of its meningitis/encephalitis panel. Its only syndromic meningitis/encephalitis PCR panel is **CSFME, CSF-only**. For blood, Mayo offers (a) two true multi-organism blood PCR/sequencing panels — **TIKLB** (tick-borne, whole blood) and **BRBST** (tick-borne bacterial sequencing, whole blood) — and (b) a set of **single-organism** blood/serum/plasma PCRs (West Nile, Powassan, Heartland, HSV, enterovirus, HHV-6, CMV-plasma, dengue/chikungunya/Zika-serum) that must be ordered individually. There is no Mayo blood panel that reproduces the CSFME 14-organism list.

**On the user's expectation of different panels by country: the record does NOT support a country-specific Mayo catalog.** Mayo describes one open-access catalog, updated daily, whose tests for Mayo patients are "available to patients around the world through Mayo Clinic Laboratories," shipped to Rochester from 80–130+ countries. What *does* differ by place is: (1) **within the US, Rochester vs Jacksonville duplicate IDs** for the same assay; (2) **New York State availability** (CSFME and the CSF arbovirus antibody panel are NOT available for NY-origin specimens, while most blood PCRs are); (3) **exposure-based branching in Mayo's own algorithms** (US vs outside-US mosquito exposure changes which tests are considered, not the catalog); and (4) **non-Mayo panels used on-site abroad** — notably QIAstat-Dx ME (15 targets, Europe) vs BioFire FilmArray ME (14 targets, = CSFME), both CSF-only. A clinician abroad who reports a "meningitis panel" with a different organism list is almost certainly reporting a local/on-site panel, not a different Mayo panel.

**On "ARBO": there is no Mayo test ID `ARBO`.** The closest Mayo IDs are **ARBOP** (serum arbovirus *antibody* panel, IFA — not PCR) and **ABOPC** (CSF arbovirus antibody panel, IFA). `ARBO`/`ARBS` appear as *local client/EHR* codes that map to Mayo ARBOP, which is a likely source of confusion. Do not order or cite `ARBO` as a Mayo PCR panel.

**Confidence / verification flag:** All Mayo facts below are from Mayo's official catalog/algorithm pages as indexed/crawled 30 Oct–2 Nov 2026. The live research browser window failed twice (`page_gone`, no tabs), so these are **index-verified, not live-window-verified**. No fact below depends on a single aggregator; client test-catalog mirrors (mml, microbiology, pediatric) reproduce the same Mayo IDs, specimen types and organism lists.

## Findings

### 1. US blood encephalitis PCR panels — exact names, IDs, specimens

#### 1A. The one syndromic panel — and why it is NOT a blood panel

| Test ID | Exact catalog name | Specimen | Method | Organisms (14) | NY |
|---|---|---|---|---|---|
| **CSFME** | Meningitis/Encephalitis Pathogen Panel, PCR, Spinal Fluid | **CSF only** — sterile vial, 1 mL, refrigerated ≤7 days; frozen specimens and shunt fluid rejected | Multiplex PCR (BioFire FilmArray) | Bacteria: *E. coli* K1, *H. influenzae*, *L. monocytogenes*, *N. meningitidis* (encapsulated only), *S. agalactiae*, *S. pneumoniae*. Viruses: CMV, enterovirus, HSV-1, HSV-2, HHV-6, human parechovirus, VZV. Fungus: *Cryptococcus neoformans/gattii* | **No** |

Source: https://www.mayocliniclabs.com/test-catalog/Overview/622764 (index, crawled 2026-11-02). Mayo states it is "not usually recommended" to concomitantly order CMVPV, LENT, HSVC or VZVPV if CSFME is ordered, and that local public-health requirements may require additional testing on positives (retain an aliquot).

**Meningitis angle (added follow-up):** the same conclusion holds for meningitis specifically. There is no Mayo "meningitis PCR, blood" panel. The meningitis workup in Mayo's Meningitis/Encephalitis Panel Algorithm (acute, <8 days) starts with lumbar puncture + CSFME if on-site CSF testing is available, plus **blood cultures** (culture, not PCR), CSF cell count/protein/glucose, Gram stain and bacterial culture. Source: https://www.mayocliniclabs.com/en/articles/resources/-/media/it-mmfiles/special%20instructions/a/a/5/meningitis-encephalitis_panel_algorithm.pdf

#### 1B. True multi-organism BLOOD panels (PCR) — the only blood "panels" in the catalog

| Test ID | Exact catalog name | Specimen | Organisms covered | Notes / limits |
|---|---|---|---|---|
| **TIKLB** | Tick-Borne Panel, Molecular Detection, PCR, Blood | Whole Blood EDTA, 1 mL | BABPB *Babesia* spp. (*B. microti, B. duncani, B. divergens*, MO-1); EPCRB *Ehrlichia/Anaplasma* (*E. chaffeensis, E. ewingii/canis, E. muris eauclairensis, A. phagocytophilum*); BMIPB *Borrelia miyamotoi* (relapsing-fever *Borrelia hermsii/parkeri/turicatae* may also be detected at a different Tm) | Does **NOT** detect *B. burgdorferi* or *B. mayonii* (Lyme). NY: Yes. Source: https://www.mayocliniclabs.com/test-catalog/overview/618311 |
| **BRBST** | Tickborne Bacterial, PCR and Sequencing, Blood | Whole Blood EDTA, 1 mL | Broad 16S rRNA PCR + NGS identification of pathogenic tick-borne bacteria in blood, incl. organisms with similar presentation (e.g. *Coxiella burnetii* Q-fever, leptospirosis) | **Not first-tier** — only when routine testing is negative. Not a meningitis panel and not marketed for encephalitis. Source: https://mml.testcatalog.org/show/BRBST |

Related, **not** a blood panel: **BRBPS** Broad Range Bacterial PCR and Sequencing, Varies — sterile body fluids (incl. CSF), tissue; PCR + sequencing for bacteria/mycobacteria. Do not cite it as a blood panel.

#### 1C. Single-organism blood/serum/plasma PCRs relevant to encephalitis/meningitis (order individually)

| Test ID | Exact catalog name | Blood specimen | Organism |
|---|---|---|---|
| **WNVBL** | West Nile Virus, RNA, PCR, Molecular Detection, Blood | Whole Blood EDTA | West Nile virus lineages 1+2. Mayo text: whole-blood PCR up to 87% sensitive in acute disease vs serum 26% |
| **WNVS** | West Nile Virus, RNA, PCR, Molecular Detection, Serum | Serum, 0.5 mL | Same virus. NY: Yes. https://www.mayocliniclabs.com/test-catalog/overview/608436 |
| **WNVUR / WNCSF** | West Nile Virus, RNA, PCR — Urine / Spinal Fluid | Urine / CSF (not blood) | Same virus; urine RNA may persist ≥10 days |
| **POWVB** | Powassan Virus, RNA, Molecular Detection, PCR, Blood | Whole Blood | Powassan virus lineages 1+2, early infection |
| **POWVS / POWVC / POWVU** | Powassan Virus, RNA, PCR — Serum / Spinal Fluid / Urine | Serum / CSF / Urine | Same virus; urine may stay positive ≥7 days. POWVC: https://www.mayocliniclabs.com/test-catalog/Overview/617485 ; POWVC NY: Yes |
| **HRTVS** | Heartland Virus, RNA, Molecular Detection, PCR, Serum | Serum, 0.5 mL | Heartland virus. NY: Yes. https://www.mayocliniclabs.com/test-catalog/download-setup?format=pdf&unit_code=620057 . HRTVC is the CSF version |
| **HSVPB** | Herpes Simplex Virus (HSV), Molecular Detection, PCR, Blood | Whole Blood EDTA, 1 mL | HSV-1 + HSV-2, disseminated disease. https://microbiology.testcatalog.org/show/HSVPB . Jacksonville duplicate: LHSVB |
| **ENTP** | Enterovirus, Molecular Detection, PCR, Plasma | Plasma EDTA, 1 mL | Enterovirus (no serotyping). https://www.mayocliniclabs.com/test-catalog/Overview/89893 |
| **QHV6P** | Human Herpesvirus-6 A and B DNA Detection and Quantification, PCR, Plasma | Plasma EDTA, 1 mL | HHV-6 A/B, quantitative. NY: Yes. https://www.mayocliniclabs.com/test-catalog/overview/619925 |
| **CMVQN** | Cytomegalovirus (CMV) DNA Detection and Quantification by Real-Time PCR, Plasma | Plasma | CMV quant. (CMVPV "Varies" is body fluids incl. CSF — for plasma Mayo directs to CMVQN: https://www.mayocliniclabs.com/test-catalog/Overview/618968) |
| **DENGS** | Dengue Virus, Molecular Detection, PCR, Serum | Serum | Dengue virus — listed for outside-US mosquito exposure (see §2) |
| **CHIKS** | Chikungunya Virus, PCR, Molecular Detection, Serum | Serum | Chikungunya virus — outside-US exposure |
| **VZIKS** | Zika Virus, PCR, Molecular Detection, Serum | Serum | Zika virus — any-region exposure; VZIKU is urine |

**No blood counterpart found for these CSFME targets** (do not assume one exists): the six CSFME bacteria as a blood multiplex; human parechovirus as a standalone blood/plasma PCR; VZV as a standalone blood PCR (VZVPV "Varies" lists CSF, body fluid, swab, respiratory and tissue — blood is not listed in the definition excerpt); *Cryptococcus* by blood PCR (diagnosis on blood is antigen-based, not a Mayo blood PCR panel). See Gaps.

#### 1D. Broad / metagenomic tests that are NOT PCR panels — do not mislabel them

- **MSCSF** Bacteria, Virus, Fungus, and Parasite Metagenomic Sequencing, Spinal Fluid — CSF 2 mL, metagenomic NGS (not PCR), lumbar-puncture CSF only, shunt/ventricular fluid not acceptable, NY: Yes. https://www.mayocliniclabs.com/test-catalog/download-setup?format=pdf&unit_code=620941
- **KPLA / KDPLA** Karius Spectrum, Plasma / Direct Ship, Plasma — plasma microbial cell-free DNA metagenomic sequencing, >1,000 bacteria/fungi/DNA viruses/parasites, **performed by Karius Laboratory**, ordered through Mayo. Not a Mayo PCR panel, not encephalitis/meningitis-specific. https://www.mayocliniclabs.com/test-catalog/download-setup?format=pdf&unit_code=623289
- **FLARP** Free-Living Amebae, Molecular Detection, PCR, Varies — CSF 0.5 mL or tissue (brain/skin/lung) only; *Acanthamoeba* spp., *Naegleria fowleri*, *Balamuthia mandrillaris*; primary amebic meningoencephalitis / granulomatous amebic encephalitis. NY: Yes. https://kootenaihealth.testcatalog.org/show/FLARP — **not blood**.
- Fungal/mycobacterial add-ons in the meningitis algorithm (not blood PCR panels): HBRP *Histoplasma/Blastomyces* PCR, Varies; MTBRP *M. tuberculosis* complex PCR; HIBC Histoplasma/Blastomyces Panel, Spinal Fluid; FUNSF Fungitell CSF (1,3-β-D-glucan, not PCR).

### 2. International availability — testing the "different panels by country" expectation

**Verdict: NOT supported for Mayo's own catalog; supported for the wider ecosystem.**

Evidence for one Mayo catalog worldwide:
- Mayo Specialty Testing: "the testing used to diagnose and treat Mayo Clinic patients is available to patients around the world through Mayo Clinic Laboratories." https://test.mayocliniclabs.com/test-catalog/specialty-testing
- Mayo Global Capabilities: open-access test catalog "updated daily," MayoLINK ordering in eight languages, individualized global logistics/packaging to extend specimen stability "traveling around the world," specimens from institutions around the world arriving daily in Rochester. https://news.mayocliniclabs.com/international/global-capabilities/
- No country-specific Mayo encephalitis/meningitis PCR panel, renamed panel, or different organism list was found in the Mayo catalog, its algorithms, or client mirrors. The same IDs (CSFME, TIKLB, WNVS, ARBOP, ENS2, etc.) are reproduced by US client catalogs (Michigan, Minnesota, Wisconsin, etc.).

What actually varies — and is the likely origin of the expectation:

1. **Within the US, by performing site (not country): Rochester vs Jacksonville duplicates.** Jacksonville-only IDs, with Rochester equivalents for all other clients: LHSV/LHSVB (= HSVPV/HSVPB), LCMV (= CMVPV), LVZV (= VZVPV), LHSVZ (= HSVPV+VZVPV). A report bearing one of these IDs does not mean a different assay or a different country — it means the specimen went to Jacksonville, FL.
2. **Within the US, by state: New York.** Each Mayo page carries a "NY State Available" field. CSFME = No; ABOPC (CSF arbovirus antibody panel) = "not available for specimens originating in New York"; ARBOP (serum) = Yes; WNVS, TIKLB, ENS2, MSCSF, POWVC, HRTVS, FLARP, QHV6P = Yes. This is the only state-level panel-availability split found.
3. **By exposure geography, in Mayo's algorithms (not a separate catalog).** Mayo's Mosquito-borne Disease Laboratory Testing algorithm (Mar 2024) branches on exposure, while keeping the same test IDs: https://news.mayocliniclabs.com/n1/96e99366cea7b0de/uploads/2025/05/Mosquito-borne_Disease_Laboratory_Testing.pdf — US exposure → ARBOP/ABOPC + individual California/Eastern/St. Louis/Western panels; outside-US exposure → chikungunya (CHIKV/CHIKS/CHIKC), dengue (DENGM/DENVP/DNSAG/DENGS/DENGC), Zika (VZIKM/VZIKU/VZIKS); any region → West Nile antibody (WNS/WNC) + WNV PCR (WNVBL/WNVUR/WNVS/WNCSF). A patient with non-US exposure therefore gets a *different test selection*, not a different Mayo panel.
4. **Outside Mayo, on-site abroad: genuinely different syndromic panels under similar names.** BioFire FilmArray ME (the assay behind CSFME) = 14 targets, CSF only, used in the US, India, Morocco, etc. QIAstat-Dx ME (Qiagen, CE-IVD, introduced Europe 2022) = 15 targets: it **adds** *Streptococcus pyogenes* and *Mycoplasma pneumoniae* and **does not include CMV** (the FilmArray-only viral target in head-to-head tables). Sources (secondary literature, not Mayo): https://journals.asm.org/doi/10.1128/spectrum.05144-22 ; https://www2.mdpi.com/2075-4418/14/8/802 . Neither syndromic panel is validated for blood. This — plus local public-health/CDC arbovirus testing abroad — is the real mechanism behind "different meningitis panels in different countries."
5. **Practical international limits, not organism-list differences:** specimen stability windows (e.g. CSFME refrigerated ≤7 days; serum arbovirus panels 14 days) and customs/import logistics. Mayo's global-logistics pages address these with tailored packaging and carrier handling, not with a second catalog.

### 3a. Infectious encephalitis panels — by pathogen class

- **Viral (PCR, blood):** WNV (WNVBL/WNVS), Powassan (POWVB/POWVS), Heartland (HRTVS), HSV (HSVPB), enterovirus (ENTP plasma), HHV-6 (QHV6P plasma), CMV (CMVQN plasma), dengue/chikungunya/Zika (DENGS/CHIKS/VZIKS serum). Viral (PCR, CSF only): the CSFME viral targets above + HSVC, LENT, VZVPV, WNCSF, POWVC, HRTVC.
- **Bacterial (PCR/sequencing):** No blood meningitis multiplex. Blood: TIKLB + BRBST (tick-borne bacteria only). CSF/other: CSFME bacterial targets, BRBPS broad-range bacterial PCR+sequencing (Varies, incl. CSF), MTBRP (TB complex, Varies), LYMPV (Lyme PCR, Varies).
- **Fungal:** CSFME *Cryptococcus neoformans/gattii* (CSF PCR) is the only fungal target in a syndromic panel. No blood fungal PCR panel found; fungal workup is antigen/culture/PCR-by-organism (HBRP, CIMRP *Coccidioides* PCR, FUNSF).
- **Parasitic:** No blood parasitic encephalitis PCR panel found. CSF/tissue: FLARP (free-living amebae, CSF/tissue); PTOX/TOXB *Toxoplasma gondii* PCR, Varies/Blood — TOXB is a blood *Toxoplasma* PCR listed on Mayo's microbiology request form, but it is a single-organism test, not a panel, and its full catalog page was not verified here (see Gaps). MSCSF (CSF metagenomic NGS) can in principle detect parasites in CSF.

### 3b. Autoimmune encephalitis evaluations — ANTIBODY-based, NOT PCR (labelled)

| Test ID | Exact catalog name | Specimen | Method (antibody) | Key antibodies |
|---|---|---|---|---|
| **ENS2** | Encephalopathy, Autoimmune/Paraneoplastic Evaluation, Serum | Serum | IFA, cell-binding assay (CBA), ELISA, RIA, Western blot, immunoblot + interpretation | AMPA-R, amphiphysin, AGNA-1, ANNA-1/2/3, CASPR2, CRMP-5, DPPX, GABA-A/B-R, GAD65, IgLON5, KLHL11, LGI1, Ma2, mGluR1/5, neurochondrin, NMDA-R, PDE10A, PCA-1/2/Tr, septin-7, TRIM46, AK5. NY: Yes. https://www.mayocliniclabs.com/test-catalog/Overview/92116 |
| **ENC2** | Encephalopathy, Autoimmune/Paraneoplastic Evaluation, Spinal Fluid | CSF | Same antibody methods, CSF versions | Same antibody set in CSF form. Adult (≥18 y). https://www.mayocliniclabs.com/test-catalog/download-setup?format=pdf&unit_code=92117 |
| **PCDES / PCDEC** | Pediatric Autoimmune Encephalopathy/CNS Disorder Evaluation, Serum / Spinal Fluid | Serum / CSF | Antibody (IFA/CBA/RIA/immunoblot) | Pediatric counterpart. ENC2 ordered for <18 y is cancelled and auto-reordered as PCDEC; ENS2 likewise maps to PCDES. |

Mayo neuroimmunology guidance: order the phenotype evaluation in **both** serum and CSF for encephalopathy/epilepsy/dementia/movement disorders — some antibodies are more sensitive in one fluid (NMDA, GFAP, NIF better in CSF; LGI1, CASPR2 better in serum). Source: https://news.mayocliniclabs.com/autoimmune-testing-education/ — **None of these is a PCR test, and none should be cited as an "encephalitis PCR panel."**

### 3c. Arbovirus antibody panels — the "ARBO" clarification (ANTIBODY, not PCR)

| Test ID | Exact catalog name | Specimen | Method | Viruses |
|---|---|---|---|---|
| **ARBOP** | Arbovirus Antibody Panel, IgG and IgM, Serum | Serum, 0.5 mL | IFA | California (La Crosse), Eastern equine, St. Louis, Western equine (CAVP, EEEP, STLP, WEEP). NY: Yes. https://www.mayocliniclabs.com/test-catalog/overview/83267 |
| **ABOPC** | Arbovirus Antibody Panel, IgG and IgM, Spinal Fluid | CSF, 0.7 mL | IFA | Same 4 viruses (CAVPC, EEPC, STLPC, WEEPC). **Not available for NY-origin specimens.** https://www.mayocliniclabs.com/test-catalog/overview/83897 |

No Mayo ID `ARBO` exists. `ARBO`/`ARBS` are local client/EHR shorthand that resolves to Mayo ARBOP (e.g. Children's Minnesota lists lab code ARBS, "Referred to: Mayo Medical Laboratories (MML Test: ARBOP)"). If a record says "ARBO panel," verify whether it means ARBOP (serum antibody), ABOPC (CSF antibody), or a non-Mayo local arbovirus panel — it does not denote a Mayo PCR panel.

### 4. Panels routed to CDC / public-health laboratories; state/country restrictions

- **Bourbon virus and Jamestown Canyon virus:** Mayo's mosquito algorithm says, if suspected, "contact your local public health department or the CDC for testing options." No Mayo PCR/antibody ID for either was found. Source: mosquito algorithm PDF above.
- **Heartland virus serology:** Mayo's HRTVS definition states patients with symptoms >1 week may be PCR-negative and "may require serologic testing, which is available through the Centers for Disease Control and Prevention." (Mayo PCR itself is in-house.)
- **CSFME positives and local public health:** Mayo's CSFME page warns "there may be local public health requirements that impact MCL clients and require additional testing on specimens with positive results" and to retain an aliquot. This is a *downstream* public-health obligation, not a Mayo-to-CDC referral of the panel itself.
- **Arbovirus confirmation:** Mayo's West Nile pages note closely related flaviviruses cross-react serologically and plaque-reduction neutralization may be needed epidemiologically — the type of confirmatory work typically done by state public-health / CDC laboratories. No specific Mayo "send to CDC" panel ID for this was verified (Gap).
- **State restriction (NY):** see §2, point 2. No other US state panel ban was found in the pages reviewed.
- **Country restriction:** no Mayo country ban or country-specific panel was found. The binding international constraints found are specimen-stability windows and shipping/customs logistics (see §2, point 5), plus the fact that some tests are performed only at Rochester (or only at Jacksonville for the duplicate IDs).

## Could not verify / Gaps

1. **Live-window verification failed.** The research browser opened no tabs (`page_gone` twice). All Mayo facts are from official catalog pages crawled 30 Oct–2 Nov 2026 via the web index, cross-checked against client mirrors — strong, but not a live page read in this session. Re-check CSFME and TIKLB on mayocliniclabs.com before ordering.
2. **No Mayo blood PCR ID for:** human parechovirus (standalone), VZV (standalone blood), *Cryptococcus* (blood PCR), or the six CSFME bacteria as a blood multiplex. Absence is based on catalog/algorithm searches, not on an exhaustive Mayo catalog dump — if a new ID exists, it was not surfaced.
3. **TOXB** (*Toxoplasma gondii* PCR, Blood) appears on Mayo's microbiology request form, but its full catalog entry (specimen volume, NY status) was not opened; do not cite details beyond its name/ID.
4. **Japanese encephalitis virus and tick-borne encephalitis virus PCR/antibody via Mayo:** no Mayo ID found; these viruses appear in Mayo pages only as cross-reactivity controls for West Nile/Powassan assays. Whether state/CDC labs offer them is outside the Mayo catalog evidence gathered.
5. **QIAstat-Dx target list** is from comparative literature (ASM/MDPI), not from Qiagen's current instructions for use; the "no CMV" point rests on head-to-head tables listing CMV as FilmArray-only. Verify against the current QIAstat-Dx IFU before citing it clinically.
6. **Pricing, turnaround times and current NY status** change frequently and were not the focus; each Mayo page's "NY State Available" and "Report Available" fields should be re-checked at order time.
7. **No page instruction / injection incident:** no page encountered attempted to redirect this research or add instructions; none was followed.

## Sources

- CSFME overview (index, crawled 2026-11-02): https://www.mayocliniclabs.com/test-catalog/Overview/622764
- Meningitis/Encephalitis Panel Algorithm (Mayo PDF): https://www.mayocliniclabs.com/en/articles/resources/-/media/it-mmfiles/special%20instructions/a/a/5/meningitis-encephalitis_panel_algorithm.pdf
- Mosquito-borne Disease Laboratory Testing algorithm (Mayo PDF, Mar 2024): https://news.mayocliniclabs.com/n1/96e99366cea7b0de/uploads/2025/05/Mosquito-borne_Disease_Laboratory_Testing.pdf
- TIKLB overview: https://www.mayocliniclabs.com/test-catalog/overview/618311
- WNVS overview: https://www.mayocliniclabs.com/test-catalog/overview/608436
- POWVC overview: https://www.mayocliniclabs.com/test-catalog/Overview/617485
- HRTVS definition: https://www.mayocliniclabs.com/test-catalog/download-setup?format=pdf&unit_code=620057
- HSVPB (Mayo Microbiology catalog mirror): https://microbiology.testcatalog.org/show/HSVPB ; Jacksonville duplicate LHSVB: https://www.mayocliniclabs.com/test-catalog/Overview/802067
- ENTP overview: https://www.mayocliniclabs.com/test-catalog/Overview/89893
- QHV6P overview: https://www.mayocliniclabs.com/test-catalog/overview/619925
- CMVPV overview (plasma guidance): https://www.mayocliniclabs.com/test-catalog/Overview/618968
- BRBST (Mayo Rochester catalog mirror): https://mml.testcatalog.org/show/BRBST
- MSCSF definition: https://www.mayocliniclabs.com/test-catalog/download-setup?format=pdf&unit_code=620941
- FLARP (client mirror): https://kootenaihealth.testcatalog.org/show/FLARP
- Karius KDPLA definition: https://www.mayocliniclabs.com/test-catalog/download-setup?format=pdf&unit_code=623289
- ARBOP overview: https://www.mayocliniclabs.com/test-catalog/overview/83267
- ABOPC overview: https://www.mayocliniclabs.com/test-catalog/overview/83897
- ENS2 overview: https://www.mayocliniclabs.com/test-catalog/Overview/92116
- ENC2 definition: https://www.mayocliniclabs.com/test-catalog/download-setup?format=pdf&unit_code=92117
- Autoimmune testing education (Mayo Insights): https://news.mayocliniclabs.com/autoimmune-testing-education/
- Mayo Specialty Testing (worldwide availability statement): https://test.mayocliniclabs.com/test-catalog/specialty-testing
- Mayo Global Capabilities: https://news.mayocliniclabs.com/international/global-capabilities/
- QIAstat-Dx vs FilmArray comparison (ASM): https://journals.asm.org/doi/10.1128/spectrum.05144-22 ; MDPI comparison: https://www2.mdpi.com/2075-4418/14/8/802
- Working notes: notes/source-csfme.md, notes/source-blood-pcr.md, notes/source-arbo-autoimmune-international.md
