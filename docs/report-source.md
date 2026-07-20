# Report source — Assignment 2: Team Project Proposal

Canonical content source for the deck. **Every claim on a slide must trace to something on
this page.** Transcribed from the submitted Assignment 2 report.

**Title:** A centralised online Satellite Filing and Licensing (SFL) Platform for IMDA
**Stakeholder audience:** IMDA (statutory board — objective is structural viability, not profit)

---

## Executive summary

Singapore's growing space industry requires an efficient and responsive regulatory process to
support satellite orbital slot licensing. IMDA's current email-based application process
relies on manual document submissions and administrative checks, producing inconsistent
application formats, delayed error detection, and repeated clarification between applicants
and officers. These increase processing effort and may delay deployment of satellite services.

The proposal is a centralised online Satellite Filing and Licensing Platform: a single digital
submission channel that guides applicants through filing requirements while supporting IMDA's
existing regulatory role. Structured submissions and early validation improve application
quality and reduce administrative work before applications reach officers.

---

## 1. Introduction

### 1.1 Background

- The **National Space Agency of Singapore (NSAS)** was established under MTI to capture a
  share of the global space economy and is mandated to develop local capabilities and a
  space-technology ecosystem [1].
- **IMDA** is the official **notifying administration** managing local satellite orbital slot
  applications [2].
- **Orbital slots** are designated physical tracks plus corresponding radio frequencies,
  allocated to prevent mechanical or electromagnetic interference; they are finite and must be
  registered with the **ITU** [3].
- Corporate entities **cannot file directly with the ITU** — IMDA evaluates and formally
  submits on behalf of firms operating in Singapore [3].
- Applicants compile a submission package in **three categories** [4]:
  1. **Technical** — satellite characteristics matching ITU software specifications
  2. **Corporate** — legal files detailing ownership and board structures
  3. **Financial** — viability records proving capital stability
- The package is **manually bundled and emailed** to an IMDA industry liaison officer [4].

### 1.2 Problem

- Guidelines mandate specific corporate and financial disclosures but **do not prescribe
  standardised document templates or data schemas**, so formats vary case to case [5].
  Officers spend substantial time manually reviewing and interpreting different formats.
- Email channels **lack automated validation**. Document omissions or incorrect ITU software
  configurations remain undetected while the application sits in the queue, and are discovered
  only when an officer opens the application — triggering long back-and-forth clarification
  chains that drag out approval timelines and risk costly launch delays.

### 1.3 Purpose

Digitalise Singapore's satellite orbital slot licensing process to establish a highly
responsive regulatory workflow: maximise administrative efficiency for regulatory officers and
accelerate launch and deployment timelines for local space-technology firms.

---

## 2. Literature review

### 2.1 Digital government precedents in Singapore

- **Singpass** — national digital identity service; **5 million users**, **more than 2,700
  services**, **800 agencies and businesses** [6].
- **Myinfo** — lets users consent to reuse data the government already holds, removing
  repeated form filling and re-verification [7]. For IMDA, the same approach could pre-fill
  company particulars through **Corppass and ACRA**.
- **GoBusiness** — national portal for business registration, licences and grants; **more than
  120 government e-services**, **more than 200 e-Advisers**, **over 6 million
  government-to-business transactions** [8]. Shows a licensing portal can guide applicants
  through requirements **while the agency keeps control of the decision**.
- **Lesson:** use structured forms and verified data to reduce routine checks, while leaving
  eligibility decisions with officers.

### 2.2 FCC ICFS and commercial spectrum-management systems

- The **FCC** runs the **International Communications Filing System (ICFS)**. Satellite
  earth-station and space-station licence applications are submitted electronically via
  **Form 312**; **paper filing is not accepted** [9].
- ICFS **records the filing fee, assigns a file number, and routes the application
  electronically to an analyst** for initial review [9], [10].
- The FCC **may dismiss incomplete applications** or request more information. Complete
  applications proceed to public notice and legal, technical or financial review before final
  action is recorded in ICFS [10].
- The FCC publishes **checklists, templates and process guidance** for applicants [11].
- **Contrast:** IMDA receives a document package by email; ICFS receives structured electronic
  submissions. ICFS creates a reference number and routes the case as soon as it is filed,
  while an IMDA officer must first open and review email attachments.
- **Transferable features** (not US rules): structured fields, a tracking reference, early
  completeness checks, electronic routing. IMDA would still need its own checks on ownership,
  financial viability, insurance and ITU data [5].
- **Commercial vendors:**
  - **LS telcom `mySPECTRA`** (Germany) — applicant portal plus internal module for managing
    applications, coordination, billing and licence issue [12].
  - **ATDI `ICS Portal`** — e-licensing for online applications, document management, billing
    and workflow automation [13].
  - These are foreign commercial products, **not complete replacements** for IMDA's process.
    They show the technical workflow already exists in the market; IMDA would configure it
    with local rules and connect it to Corppass and ACRA.
- **Combined approach:** local digital identity and data services for applicant details +
  ICFS-style workflow for filing management + configured spectrum-management tools for
  technical checks — **without transferring regulatory judgement away from IMDA**.

---

## 3. Proposed improvements

### 3.1 Recommendation

A centralised online **Satellite Filing and Licensing Platform** combining proven Singapore
digital-government components with commercially available spectrum-management software
[12], [13], configured to IMDA's orbital-slot and ITU-filing requirements.

**Four objectives:**
1. **Consolidate the two current email channels** — licence applications to IMDA's licensing
   inbox [5], and separate ITU network filings in **SpaceCap** format to its spectrum
   administrator [14].
2. **Shift checking from post-submission review to point-of-entry validation**, closing the
   gap where errors go undetected until an officer opens the file.
3. **Reuse corporate data the government already holds**, with a guided template for data it
   does not [7].
4. **Reserve officer time for merits-based judgement** by the Authority [5].

**Four validation tiers:**

| Tier | Name | What happens |
| --- | --- | --- |
| **1** | Identity | Applicant authenticates through **Corppass, secured by Singpass** [15], as a representative of a Singapore-registered entity [5] |
| **2** | Corporate & financial | *Hybrid.* With consent, **Myinfo Business autofills ACRA-held corporate identity data**: UEN, shareholding, paid-up capital, appointment holders [7], [15]. Financial evidence (audited accounts, projections, **NPV-at-10%**, **IRR**) exists in no reusable government dataset and **cannot come from IRAS — tax secrecy** [16]. So an **FCC-style guided financial template** [11] recomputes these figures from applicant inputs and checks arithmetic, consistency and thresholds **without approving them** |
| **3** | Technical | ITU technical file passed to a **commercial off-the-shelf engine** (mySPECTRA or ICS Portal) [12], [13] for format, completeness and preliminary interference checks |
| **4** | Officer judgement | Only a complete, validated package reaches an IMDA officer for **final merits-based judgement**, mirroring ICFS's routing of completed filings to an analyst [10] |

**Tiers 2 and 3 operate as a loop:** the platform **flags errors instantly but never corrects
them**; the applicant fixes and resubmits until every check passes, so officers never receive
incomplete submissions.

**MVP (to lower risk)** — deliver the most rule-based elements first: Corppass login, identity
autofill, the guided template with automated checking, and a dashboard with an **ICFS-style
tracking reference and live status updates** [10].

### 3.2 Methods to evaluate effectiveness

- **Adoption risk is low:** builds on infrastructure applicants already use (Corppass, IMDA's
  existing **IRIS portal** [17]); peer regulators have already made the transition (mandatory
  ICFS filing; commercial licensing portals) [9], [13].
- **Uptake rate** — share of filings arriving through the platform rather than email.
- **Target: 30% reduction in officer effort — "a target to be validated, not an established
  result."** Basis: the contrast between ICFS's structured intake and IMDA's manual email
  process [9], [10], with a GoBusiness-style single window reducing back-and-forth [8].
  A **baseline study of officer time logs** measures how much work is automatable. The target
  assumes **~40% is automatable, with the platform removing roughly three quarters of that**;
  both figures checked against published e-permitting outcomes [18], [19] and revised after
  the MVP.
- **Median cycle time** from submission to decision. Cycle-time gains should exceed the effort
  target, because validation removes whole correction rounds rather than shortening them.
  **No time figure is set without a baseline.**
- **First-Time-Right (FTR) rate** — share of applications clearing validation at first
  submission; directly measures the late-discovered errors identified in Section 1.
- **Applicant benefit** — waiting times, resubmission counts, satisfaction surveys of
  applicants and officers.

### 3.3 Benefits

**3.3.1 For IMDA.** A predictable, auditable workflow strengthens IMDA's reputation as an
efficient notifying administration, with the ITU and with the industry it regulates. Slow
approval is a documented barrier for space firms [20]; lowering it should encourage more
companies to apply and experiment, growing the ecosystem IMDA and NSAS are mandated to
develop [1].

**3.3.2 For applicants.** Shorter, more predictable processing reduces launch delays [20].
**ITU registration is first-come** — earlier filings receive protection from later ones,
improving orbital-slot priority [14]. Predictable timelines reduce financing costs for firms
waiting to launch and support Singapore's space economy [1]. A process applicants can trust
makes firms more willing to approach IMDA with new missions.

### 3.4 Limitations

**3.4.1 Commercial engine constraints.** Engines were chosen because they already perform the
ITU-format and interference checks IMDA needs, are proven with peer regulators [13], and avoid
rebuilding existing capability. But built for general spectrum-management standards [12], they
**do not encode Singapore-specific rules** — ownership threshold, NPV-at-10% test, insurance
requirement [5] — so officers would inherit those unchecked, and applicants could clear
validation while still incomplete.

*Mitigations:* the engine performs only checks identical for every regulator; Singapore-specific
rules run as **separate platform checks IMDA can update directly**; during early rollout the
engine **only flags issues for officers to verify** until its accuracy is confirmed.
*Residual risk:* vendor dependence. The proposal should still proceed — **no engine output
decides an application**, so a gap in the engine reduces automation coverage, not decision
quality.

**3.4.2 Cost, borne by public funds.** Implementation and maintenance span integrations with
Corppass, Myinfo Business and the engine, GovTech onboarding, PDPA-compliant data handling
[15], [16], security upkeep and staff training. IMDA bears this even if uptake is slow.
*Mitigation:* phased rollout — the MVP delivers highest-value features first, and automation is
added only when usage data justifies it, so spending follows demonstrated demand.
*Justification:* the status quo carries its own growing cost in officer hours and reputational
risk (Table 1).

---

## 4. Conclusion

The current process relies on manual email submissions, producing inconsistent formats,
repeated clarification requests, and unnecessary administrative effort for officers and
applicants. The proposed platform addresses this through structured digital submissions,
automated validation, and integration with existing government digital services — improving
the quality and consistency of applications before they reach officers **while preserving
regulatory judgement**. Implementation requires significant investment and organisational
change, manageable through a phased rollout.

---

## Appendix — Table 1: comparison of alternative implementation approaches

| Option | Desirability | Technical feasibility | Structural viability |
| --- | --- | --- | --- |
| **Integrate existing components (recommended)** | **High** — instant feedback, a single submission channel, and a login businesses already use | **High** — reuses proven Corppass/Myinfo Business APIs [7], [15] and market-ready COTS engines [12], [13] | **High** — lower build and maintenance burden; aligns with Singapore's existing digital-government systems |
| **Status quo (do nothing)** | **Low** — existing delays and applicant frustration continue | **N/A** — no new technical system introduced | **Low** — retains fragmented processes and manual workload |

---

## References (IEEE) — canonical numbering

Slide brackets must match these numbers exactly.

1. National Space Agency of Singapore, "Singapore Space Ecosystem." https://www.space.gov.sg/singapore-space-ecosystem/singapore-space-ecosystem/
2. National Space Agency of Singapore, "IMDA Spectrum Requirements." https://www.space.gov.sg/singapore-space-ecosystem/imda-spectrum-requirements/
3. Info-communications Media Development Authority, "Guidelines on Satellite Network Filing." https://www.imda.gov.sg/-/media/imda/files/regulation-licensing-and-consultations/licensing/licenses/guidesatellitenetworkfiling.pdf
4. Info-communications Media Development Authority, "Licence for the Use of Satellite Orbital Slot." https://iris.imda.gov.sg/application/licence-for-the-use-of-satellite-orbital-slot
5. Info-communications Media Development Authority, "Guidelines on the Submission of Application for the Grant of Licence for the Use of Satellite Orbital Slot," Version 2, 23 Sep. 2025. https://www.imda.gov.sg/-/media/imda/files/regulation-licensing-and-consultations/licensing/licenses/guidesatelliteorbitalslotlic.pdf
6. Government Technology Agency of Singapore, "Singpass." https://www.tech.gov.sg/products-and-services/for-citizens/digital-services/singpass/
7. World Bank, "How Singapore's national digital identity and government digital data sharing platform fosters inclusion and resilience," 2024. https://blogs.worldbank.org/en/digital-development/how-singapores-national-digital-identity-and-government-digital-data-sharing
8. Government Technology Agency of Singapore, "GoBusiness." https://www.tech.gov.sg/products-and-services/for-businesses/corporate-transactions/gobusiness/
9. Legal Information Institute, "47 CFR § 25.110 — Filing of applications, fees, and number of copies." https://www.law.cornell.edu/cfr/text/47/25.110
10. Legal Information Institute, "47 CFR § 1.10014 — What happens after officially filing my application?" https://www.law.cornell.edu/cfr/text/47/1.10014
11. Federal Communications Commission, "Part 25 Space Station Licensing Process and Timeline." https://www.fcc.gov/part-25-space-station-licensing-process-and-timeline
12. LS telcom, "mySPECTRA." https://www.lstelcom.com/en/products/spectrum-management/myspectra/
13. ATDI, "End-to-end automated spectrum management solutions." https://atdi.com/products-and-solutions/automated-spectrum-management/
14. Office for Space Technology & Industry, "Singapore Space Industry Directory 2025/2026." https://isomer-user-content.by.gov.sg/301/42d28cd6-28e9-4717-a73c-d29274032f7a/Singapore_Space_Industry_Directory_2025_2026_Web_Version.pdf
15. Government Technology Agency of Singapore, "Myinfo Business," Corppass. https://docs.corppass.gov.sg/products/myinfo-business
16. Singapore Statutes Online, Income Tax Act 1947, 2020 Rev. Ed., s. 6, "Official secrecy." https://sso.agc.gov.sg/Act/ITA1947
17. Info-communications Media Development Authority, "Licence for the Use of Satellite Orbital Slot," IRIS e-services. https://iris.imda.gov.sg/application/licence-for-the-use-of-satellite-orbital-slot
18. A. Silver, "How Governments Are Using AI and GIS to Fast-Track Permits," Government Technology, Jul. 11, 2024. https://www.govtech.com/artificial-intelligence/how-governments-are-using-ai-and-gis-to-fast-track-permits
19. South Carolina Department of Health and Environmental Control, "The Benefits of Increased Efficiency." https://www.epa.gov/sites/default/files/2018-06/documents/dhec-final-report-508.pdf
20. Fast Company, "Space startups' biggest challenge for takeoff: Getting regulatory approval," 2024. https://www.fastcompany.com/91139334/space-wait-a-year-for-satellite-approval
