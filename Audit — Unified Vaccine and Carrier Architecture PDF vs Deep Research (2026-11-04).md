# Discriminative Audit — Unified Vaccine & Carrier Architecture Master Reference V2_30 (PDF, uploaded Nov 4, 2026) vs. Pneumococcal Deep Research (Nov 4, 2026)

- Source audited: `~/workspace/user/files/Unified_Vaccine_and_Carrier_Architecture_Master_Reference_V2_30_zv7g.pdf`, titled "Unified Vaccine & Carrier Architecture: Master Reference 3H4", described in the PDF as synthesized across cross-platform AI collaboration (Google, Meta, auxiliary tools).
- Comparator: deep research report `~/workspace/research_notes/pneumococcal-vaccine-serotype-research-20261104-1812/report.md`, plus the pneumococcal page built from it.
- Method, per Douglas's discriminative rule: item by item, deeper check against the deep research only where that research covers the item. Items outside the deep research scope are marked GAP-in-scope, not assumed false and not assumed true.
- Original PDF untouched. This audit is a new file, old-with-new. Nothing in the PDF was adopted into the pneumococcal page by this audit alone.

## Verdict summary
- HOLDS where the PDF matches the deep research: CRM197 as a diphtheria-toxin mutant carrier; Synflorix's mixed carriers (protein D, TT for 18C, DT for 19F); pneumococcal serogroup system as antigenic, not genetic; Cryptococcus GXM capsule with no licensed human vaccine and investigational GXM-carrier conjugates as a concept.
- BREAKS / MISLEADING where the PDF over-generalizes or mislabels: pneumococcal carrier mapping presented as if TT-18C / DT-19F apply to all pneumococcal vaccines; Bexsero labelled "OMV Pneumococcal"; fungal-bacterial bridge presented as proof of identical chemistry; wzx/wzy + CAP genes presented as conserved machinery across kingdoms.
- GAP-in-scope for most non-pneumococcal rows: Hib, typhoid, GBS, Salmonella, Candida/Aspergillus, influenza, HPV, and combination platforms were not covered in detail by the pneumococcal deep research, so this audit cannot verify them from that comparator — they need their own sourced check before use in a book or paper.

## Item by item

### 1. Pneumococcal carrier mapping — BREAKS as written, HOLDS for Synflorix only
- PDF claim: pneumococcal carriers = CRM197 (Prevnar, "Unites Diphtheria", Pneumosil), TT (18C), DT (19F), Protein D.
- Deep research (§2): CRM197 for all serotypes in PCV7, PCV10-SII (Pneumosil), PCV13, PCV15, PCV20, PCV21. Mixed carriers — protein D for 1, 4, 5, 6B, 7F, 9V, 14, 23F; tetanus toxoid for 18C; diphtheria toxoid for 19F — are Synflorix (PCV10-GSK) only, confirmed by EMA, Egypt PAR, and SmPC.
- Verdict: Do NOT read the PDF row as "pneumococcal vaccines use TT for 18C and DT for 19F." In PCV13/15/20, 18C and 19F are CRM197-conjugated. The PDF row collapses a Synflorix-specific mapping into a class-wide mapping.
- Garble note: "Unites Diphtheria" in the PDF text is unreadable as a brand/manufacturer — do not quote it as a name until the PDF source is re-checked.

### 2. Diphtheria and tetanus as carrier sources — HOLDS in principle
- PDF: diphtheria has no capsular serotypes, tox+ vs tox-; DT itself is the source of the CRM197 mutant link. Tetanus is toxin-only, TT as carrier.
- Deep research (§2): CRM197 is a non-toxic mutant of diphtheria toxin, Corynebacterium diphtheriae C7, and is the carrier concept across the PCVs listed above.
- Verdict: HOLDS. The PDF's cross-links from DT/TT to pneumococcal 18C/19F hold only through Synflorix (see item 1), not through all pneumococcal vaccines.

### 3. Pneumococcal serotype count and serogroup meaning — HOLDS, with a naming warning
- PDF: 100+ capsular serotypes (Quellung reaction).
- Deep research (§4): 107 serotypes in the current count, nine new since 2020, and the Danish/Quellung serogroup is antigenic, not a cps-locus cluster — six serogroups split across genetic subclusters.
- Verdict: HOLDS for "100+", and the PDF's use of serogroup as an antigenic grouping is consistent. Any table that treats serogroup as a genetic cluster would break — the PDF does not explicitly do that in the readable text, but its "Genetic Conservation" insight (item 10) risks it.

### 4. Meningococcal row — HOLDS on serogroups, BREAKS on Bexsero label
- PDF: serogroups A, B, C, W, Y, X; Group A ManNAc-1-P, C/W/Y sialic acid variations; DT (Menactra), CRM197 (Menveo), TT (MenQuadfi), "OMV Pneumococcal (Bexsero)".
- Deep research (§5.4): meningococcal serogroups A, B, C, W135, X, Y are a parallel capsule-serotyping system, not pneumococcal relatives.
- Verdict: Serogroup list HOLDS in substance. "OMV Pneumococcal (Bexsero)" BREAKS: Bexsero is a meningococcal B vaccine with outer membrane vesicles — it is not pneumococcal. Do not copy that cell.
- Garble note: "Shares identical carrier footprint with and Hib vaccines" is an incomplete sentence in the PDF extraction — do not quote it as a claim.

### 5. Hib, typhoid, GBS, Salmonella rows — GAP-in-scope, not verified by this comparator
- PDF claims: Hib a–f, PRP, TT (ActHIB), CRM197 (HbOC), OMP (PedvaxHIB); typhoid Vi, TT (Typbar-TCV), CRM197 (Vi-CRM); GBS Ia, Ib, II, III, IV, V, sialic-acid based, CRM197 in investigational GBS6; Salmonella Kaufmann-White O/H, LPS O-antigen, TT/CRM197/DT.
- Deep research: Hib a–f and GBS are mentioned only as parallel capsule systems (§5.4). Typhoid and Salmonella are not covered in detail.
- Verdict: GAP for this audit. No contradiction found in the deep research, and no confirmation either. The GBS row in the PDF is also split across pages in extraction, so its carrier cell ("CRM197 (in investigational GBS6), TT, native proteins") is not cleanly readable — re-check the PDF source before quoting it.

### 6. Fungal row — Cryptococcus — HOLDS on capsule and no licensed vaccine, BREAKS on "proves identical chemistry"
- PDF: Cryptococcus neoformans/gattii, GXM capsule with mannose backbone, CAP genes (CAP10, 59, 60, 64 in extraction), no licensed human vaccine, investigational GXM-TT, GXM-DT, GXM-CRM197, "The Fungal-Bacterial Bridge: Proves use identical chemistry and carrier logic to bacteria."
- Deep research (§5.4): Cryptococcus capsules are GXM (+ galactoxylomannan), serotypes A, D, AD (neoformans/grubii) and B, C (gattii), defined by GXM reactivity. There is NO mapping of pneumococcal serogroups onto fungal serotypes. The only retrieved bridge is an unnamed "some antigenic determinants shared with certain pneumococcal polysaccharides" — GAP for any per-serotype fungal relationship.
- Verdict: Capsule, CAP-gene family, and no-licensed-vaccine points HOLD in general terms. "Proves identical chemistry" BREAKS: GXM is not identical chemistry to pneumococcal repeat units, and carrier logic (conjugating a polysaccharide to TT/DT/CRM197) is a shared design concept, not proof of identical chemistry or a serogroup relationship. For a book/paper, write "shared carrier design concept, investigational" — not "proves identical chemistry."
- Note: PDF's CAP list reads "CAP10, 59, 60, 64" in extraction; the deep research does not enumerate CAP genes, so that list is GAP-in-scope for this audit.

### 7. Candida / Aspergillus, influenza, HPV rows — GAP-in-scope, analogy only
- PDF: Candida/Aspergillus mannan, beta-glucan, galactomannan, Als3, NDV-3A, PEV7, Sap2, CRM197 wall trials; influenza HA/NA, 8 RNA segments, no toxoid carrier; HPV L1 VLPs, no carrier, genotype numbers parallel bacterial serotypes.
- Deep research: none of these are covered in detail, except the general point that viral glycoproteins and VLPs are not polysaccharide serotypes.
- Verdict: GAP for this audit. The HPV "genotype numbers parallel bacterial serotypes" is an analogy, not a documented relationship — do not present it as a serotype mapping.

### 8. Combination platforms — GAP-in-scope
- PDF: DT/Td/DTaP/Tdap, Menitorix (MenC-TT / PRP-TT sharing TT), MMR/MMRV, Twinrix.
- Deep research: combination platforms are not covered.
- Verdict: GAP for this audit. Menitorix sharing TT is plausible as a carrier-sharing example, but it was not verified against a label in this audit — check it separately before print.

### 9. Carrier Trinity and CIES — HOLDS as concepts, PARTIAL as documented claims in this comparator
- PDF: DT, TT, CRM197 convert T-independent polysaccharides into T-dependent neoantigens; carrier-induced epitopic suppression (CIES) can accelerate clearance or crowd out B-cell activation, managed by carrier diversification (Protein D, OMPC).
- Deep research: carrier proteins are documented per vaccine (§2), and carrier diversification (e.g., Synflorix protein D) is documented as a design choice. CIES itself is not audited in the deep research report.
- Verdict: Concepts HOLD in general vaccinology, PARTIAL in this audit — do not cite the deep research as the source for CIES; cite a CIES-specific source if used in print.

### 10. Genetic conservation across kingdoms — BREAKS as written
- PDF: "Homologous machinery (wzx/wzy in bacteria, CAP genes in fungi) governs capsule assembly across kingdoms."
- Deep research: wzx/wzy are bacterial capsule-assembly genes; CAP genes are fungal capsule genes. The deep research treats bacterial cps loci and fungal GXM as parallel systems, not homologous machinery, and warns against merging capsule systems (§4.4, §5.4).
- Verdict: BREAKS as a homology claim. Parallel function (both make a capsule) is not homology (same machinery). For print, write "parallel capsule-assembly systems in bacteria and fungi" — not "homologous machinery across kingdoms."

## Addendum — Provenance and 99% belief, Nov 4, 2026, ~2:34 PM CST (his account)
- Douglas's account, in substance: the PDF was built with deep thinking Google Gemini, with fact check involved, and deep research mode, so he believes the information is 99% verified on the PDF he gave Ember.
- Filed as HIS belief and HIS provenance account, NOT as Ember's verification. The audit's BREAKS above (Synflorix-only TT/DT mapping, Bexsero label, "proves identical chemistry", wzx/wzy–CAP homology) remain as audit findings against the extracted PDF text and the deep research comparator, side by side with his belief — they are not erased by the provenance account.
- Open reconciliation, not assumed: it is possible some audit breaks are extraction garble rather than PDF originals (the PDF extraction already showed garbled/split cells). The next check, if he directs it, is to re-read those four cells directly in the PDF source itself, before changing either the audit verdict or his 99% belief. Until that re-read, the status is: his belief = 99% verified [H]; audit breaks = found in extracted text vs deep research [D vs PDF-text]; GAP-in-scope items = still GAP for this comparator.

## What this audit does NOT do
- It does not verify the non-pneumococcal rows (Hib, typhoid, GBS, Salmonella, fungi beyond Cryptococcus, viruses, combinations) — those need their own sourced audit.
- It does not adopt the PDF into the pneumococcal page. If Douglas directs an addition, only the HOLDS items above should be added, with the item-1 and item-4 corrections applied, and GAP items left GAP.
- It does not resolve which serotype in Douglas's serogroup table came from a single website — that serotype was unnamed, and this PDF is not asserted to be that source.
