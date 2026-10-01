# PP-SPEC-034: Proof of Efficacy Mapping to OWASP AIVSS

| Field | Value |
|---|---|
| Status | DRAFT v0.1 |
| Author | Craig Ellrod, Nebulonium, Inc. (dba HACKERverse®) |
| Date | October 1, 2026 |
| License | CC BY-ND 4.0 |
| Maps to | OWASP AI Vulnerability Scoring System (AIVSS), including the current Agentic AI scoring methodology |
| Series | Proof Protocol Framework Mapping Specifications |

---

## 1. Purpose

This specification documents how an AIVSS-scored AI vulnerability or risk can be used to select, prioritize, and contextualize Proof Protocol efficacy testing without replacing AIVSS scoring.

The referenced external framework remains authoritative for its own terminology, requirements, scoring, controls, or architecture. This document defines a **Proof Protocol mapping**; it does not claim ownership of, modify, or supersede the referenced framework.

## 2. Scope

This specification covers AIVSS findings, scores, risk categories, and mitigation context used as inputs to Proof of Efficacy. Proof Protocol does not recalculate or supersede the authoritative AIVSS score.

It defines **what is measured**, **how the external framework is bound to a Proof Protocol test**, and **what evidence is produced**. Independent witnessing and evidence-capture implementation are defined elsewhere in the Proof Protocol specification family.

## 3. The Core Question

Proof of efficacy answers one question about any control:

> **Was there a control, and did it work?**

For this mapping, that question is applied to a control, safeguard, design assertion, policy, identity claim, or mitigation associated with **OWASP AIVSS**.

- **Control:** any safeguard, mitigation, or protocol intended to prevent, detect, or respond to a harm.
- **Attestation:** evidence produced by, or inside the control of, the party being assessed. Attestation can establish that a control exists. It cannot establish that the control works.
- **Proof:** evidence corroborated by one or more parties structurally independent of the party being assessed. Structural independence is a hard requirement for valid corroboration.
- **Proof of Efficacy:** corroborated evidence that a specific control, under adversarial conditions similar to deployment, performed as claimed.
- **Independent Proof of Efficacy Organization (IPEO):** a structurally independent party that produces Proof of Efficacy.

## 4. Metric Definitions

All metrics are computed against a **defined test corpus**: a documented set of adversarial cases, paired with benign cases where applicable.

| Metric | Definition |
|---|---|
| **Efficacy score** | For every adversarial case, the result is recorded as **blocked**, **detected**, **missed**, or **INVALID**. |
| **Containment rate** | Share of adversarial cases the control blocked. |
| **Detection rate** | Share of adversarial cases the control identified, whether or not it blocked them. |
| **Miss rate** | Share of adversarial cases the control neither blocked nor identified. |
| **False-positive rate** | Share of paired benign cases the control wrongly blocked or flagged. |
| **Robustness** | Results for cases attempting to suppress, evade, bypass, or manipulate the control. |
| **Version-level results** | Metrics reported per version of the system and control under test. |
| **Invalid-result status** | **INVALID** when required evidence is incomplete or broken; never counted as a pass. |

**Target levels.** Acceptable levels and target values are defined per engagement and risk category. They are not fixed by this mapping specification.

## 5. Evidence Produced

| Artifact | Description |
|---|---|
| **Proof record** | One record per test case: control, system/version, case, verdict, timestamp, and evidence references. |
| **ProofStamp™** | Trusted timestamp bound to a verdict/evidence object so a third party can verify time and integrity. |
| **ProofBundle™** | Packaged proof records, timestamps, metric results, corpus manifest, and environment/context for an engagement. |
| **ProofRegister™** | Public register of issued proof records. |
| **Corpus manifest** | Case categories, counts, benign pairings where applicable, and corpus version. |

## 6. Mapping to OWASP AIVSS

External-framework text is summarized or described at a high level. Consult the authoritative framework for its exact wording and current version.

| OWASP AIVSS element | Proof Protocol mapping | Evidence |
|---|---|---|
| **AIVSS finding** | The vulnerability/risk identifier is bound to the Proof Protocol test scope. | ProofBundle™ metadata |
| **AIVSS score** | The authoritative score MAY prioritize test urgency, corpus depth, and retest cadence; the score is preserved, not recomputed. | Scope statement; ProofBundle™ |
| **Risk category** | The AIVSS category labels the relevant adversarial corpus subset. | Corpus manifest |
| **Claimed mitigation** | A control intended to mitigate the scored vulnerability becomes the control under test. | Proof record |
| **Exploit/test condition** | A test exercises the vulnerability or representative attack path under deployment-similar conditions. | Execution evidence |
| **Measured efficacy** | Control behavior is measured as blocked, detected, missed, false positive where applicable, or INVALID. | Efficacy score; proof records |
| **Post-mitigation evidence** | Proof Protocol records whether the mitigation performed as claimed; it does not assert that the underlying vulnerability no longer exists. | ProofBundle™; ProofRegister™ |

## 7. Interoperability Rules

1. The external framework identifier, version, and relevant element SHOULD be recorded in the ProofBundle™.
2. External scores, classifications, or control identifiers MUST NOT be silently recomputed or redefined by this specification.
3. A control's **presence**, **configuration**, **activation**, and **efficacy** are distinct facts and SHOULD be recorded separately when evidence permits.
4. A control firing does not by itself establish efficacy when the claim is that a downstream target was protected. Target, SIEM, vendor, application, or equivalent outcome evidence SHOULD be captured when required to establish the result.
5. Missing or broken evidence MUST produce **INVALID**, not PASS.
6. Material changes to the system, control, model, policy, environment, identity, or test corpus SHOULD trigger versioned retesting when those changes can affect the result.

## Framework-Agnostic Architecture

> **Threat frameworks are pluggable inputs to Proof Protocol. Proof Protocol is framework-agnostic.**

External frameworks can identify **what to test**: threats, vulnerabilities, controls, design assertions, identity claims, or risk conditions. Proof Protocol independently establishes **whether the control worked and what evidence proves that result**.

No external framework is required for Proof Protocol to operate. A Proof Protocol implementation MAY use MAESTRO, MITRE ATLAS, OWASP, AIVSS, a proprietary threat model, another recognized framework, or no external framework at all when the test condition is otherwise sufficiently defined.

Adding, replacing, muting, or removing a framework mapping does not alter the Proof Protocol architecture, evidence model, Proof of Efficacy determination, ProofBundle™, ProofStamp™, ProofRegister™, or independent corroboration requirements.

A framework mapping therefore establishes **interoperability**, not architectural dependency.

## 8. Relationship to Proof Protocol

This mapping is part of the Proof Protocol specification family maintained by Nebulonium, Inc. It is designed to let existing cybersecurity and AI-security frameworks supply threat, risk, control, design, identity, or testing context while Proof Protocol supplies a common evidence and efficacy layer.

The mapping is intentionally asymmetric:

> **OWASP AIVSS supplies framework context. Proof Protocol supplies the evidence model for testing whether a selected claim or control performed as claimed.**

No affiliation, endorsement, certification, or sponsorship by the maintainers of OWASP AIVSS is implied.

## 9. Source Framework, Attribution, and License

- **Referenced framework:** OWASP AIVSS
- **Owner / maintainer:** OWASP Foundation
- **Authoritative source:** https://github.com/OWASP/www-project-artificial-intelligence-vulnerability-scoring-system
- **Upstream license status:** CC BY-SA 4.0 is stated for the published AIVSS scoring document; the repository contains a LICENSE.md.
- **Proof Protocol reuse determination:** **YES, WITH CONDITIONS**

**Use in this mapping.** CC BY-SA permits sharing and adaptation, including commercial use, with attribution and ShareAlike for adapted material. Because Proof Protocol uses CC BY-ND 4.0, this mapping should reference identifiers and independently describe the crosswalk rather than incorporate adapted AIVSS text that would need to be distributed under CC BY-SA.

This license determination applies to the referenced upstream material, not to this Proof Protocol mapping specification. This mapping remains licensed under **CC BY-ND 4.0** as stated above. Framework names and trademarks remain the property of their respective owners. This section is a practical licensing assessment, not legal advice.

## 10. References

- OWASP Foundation, “AI Vulnerability Scoring System (AIVSS),” current project publication and scoring methodology.

## 11. Versioning

This mapping is versioned independently of the referenced framework. If the external framework changes materially, a new version of this specification SHOULD identify the framework version mapped and any changed mappings.

Each release SHOULD be anchored with a dated identifier and, where available, a persistent citation record.

---

*Proof Protocol · proofprotocol.io · CC BY-ND 4.0*
