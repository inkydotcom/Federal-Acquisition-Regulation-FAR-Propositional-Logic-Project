# Federal Acquisition Regulations System
# Formal Propositional and Deontic Logic Formalization

---

## Methodology

This formalization proceeds in two phases. Phase 1 reduces the regulatory text of FAR Part 1 to strict propositional logic: atomic propositions connected only by the standard connectives (∧, ∨, ¬, →, ↔). No quantifiers, no predicates with argument structure, no embedded natural language. Phase 2 layers deontic modal operators onto the propositional base to capture the normative force (obligation, permission, prohibition) of each rule.

Where the source text implies universal quantification ("all authorities may be delegated"), the corresponding formula is a propositional schema, meaning it holds for any instantiation of the relevant proposition. This is noted where applicable.

---

## Connectives

| Symbol | Meaning           |
|--------|-------------------|
| ∧      | Conjunction (and)  |
| ∨      | Disjunction (or)   |
| ¬      | Negation (not)     |
| →      | Material conditional (if...then) |
| ↔      | Biconditional (if and only if)   |

## Deontic Operators (Phase 2)

| Operator | Meaning                              |
|----------|--------------------------------------|
| O(p)     | It is obligatory that p (shall/must) |
| P(p)     | It is permitted that p (may/can)     |
| F(p)     | It is forbidden that p (shall not)   |

Standard deontic relations hold: F(p) ↔ ¬P(p) and O(p) ↔ ¬P(¬p).

---

## Atomic Proposition Table

Each atomic proposition is a simple declarative statement that is either true or false. No proposition contains internal logical structure.

### System Composition (Subpart 1.1)

| Symbol | Definition |
|--------|-----------|
| s      | The Federal Acquisition Regulations System is established |
| f      | The FAR is a component of the system |
| a      | Agency acquisition regulations are components of the system |
| g      | Acquisition guides are components of the system |
| ig     | Internal agency guidance is a component of the system |

### System Objectives (Subpart 1.1)

| Symbol | Definition |
|--------|-----------|
| m₁     | The system meets the government's mission efficiently |
| m₂     | The system maximizes commercial buying |
| m₃     | The system maintains integrity in contracting |
| m₄     | The system maintains openness in contracting |
| m₅     | The system focuses on risk management |
| m₆     | All acquisition risk is eliminated |

### Contracting Officer Properties (Subparts 1.1, 1.4)

| Symbol | Definition |
|--------|-----------|
| c      | The actor is a duly appointed Contracting Officer |
| c_auth | The CO has authority to apply the FAR |
| c_sign | The CO signs the contract |
| c_legal| The CO ensures legal compliance before signature |
| c_funds| The CO ensures funds are available before signature |
| c_fair | The CO ensures fair treatment of offerors |
| c_resp | The CO is responsible for the directed action |
| c_appt | The CO appointment is made in writing |
| c_ofpp | The CO appointment is consistent with OFPP standards |
| c_term | The CO termination is made in writing |
| c_retro| The CO termination is retroactive |

### Acquisition Strategy Properties (Subpart 1.1)

| Symbol | Definition |
|--------|-----------|
| q₁     | The acquisition strategy serves the government's best interest |
| q₂     | The strategy is addressed in the FAR |
| q₃     | The strategy is prohibited by law or regulation |
| q₄     | The strategy is used |

### Publication and Certification (Subpart 1.1)

| Symbol | Definition |
|--------|-----------|
| r₁     | A change to the FAR is proposed |
| r₂     | The change is published in the Federal Register |
| r₃     | A certification is required |
| r₄     | The certification requirement is authorized by statute |

### Delegation and Sunset (Subpart 1.1)

| Symbol | Definition |
|--------|-----------|
| d₁     | An authority is delegated |
| d₂     | Delegation is specifically prohibited by the FAR |
| d₃     | A FAR section is directed by an action |
| u₁     | The FAR section has a statutory basis |
| u₂     | The FAR section expires after four years |
| u₃     | The FAR Council renews the section |

### Agency Regulation Properties (Subpart 1.2)

| Symbol | Definition |
|--------|-----------|
| a_iss  | The agency head issues an agency regulation |
| a_rep  | The agency regulation unnecessarily repeats the FAR |
| a_con  | The agency regulation conflicts with the FAR |
| a_law  | The conflict is required by law |
| a_pub  | The agency regulation is published for public comment |
| a_cost | The regulation imposes significant cost |
| a_imp  | The regulation has significant administrative impact |

### Deviation Properties (Subpart 1.3)

| Symbol | Definition |
|--------|-----------|
| v₁     | The agency deviates from the FAR |
| v₂     | The deviation concerns CASB rules |
| v₃     | The agency head authorizes the individual deviation |
| v₄     | The CO documents the justification for the deviation |
| v₅     | The deviation is a class deviation |
| v₆     | The FAR Council approves the class deviation |
| v₇     | The FAR Secretariat is notified by email |
| v₈     | The deviation is necessary for a treaty or international agreement |
| v₉     | The deviation is inconsistent with post-treaty domestic law |

### COR Properties (Subpart 1.4)

| Symbol | Definition |
|--------|-----------|
| cor_des | The COR designation is made in writing |
| cor_del | The COR delegates authority |
| cor_asgn| A COR is assigned to the contract |
| cor_ffp | The contract is firm-fixed-price |
| cor_prc | The COR changes the contract price |
| cor_qty | The COR changes the contract quality requirements |

### Ratification Properties (Subpart 1.4)

| Symbol | Definition |
|--------|-----------|
| t₁     | An unauthorized commitment is ratified |
| t₂     | The government received a benefit |
| t₃     | Ratifying authority exists |
| t₄     | The price is fair and reasonable |
| t₅     | Funds are available for ratification |

### Determinations and Findings (Subpart 1.5)

| Symbol | Definition |
|--------|-----------|
| df₁    | A D&F is executed |
| df₂    | The D&F is a written approval |
| df₃    | The findings support the determination |
| df₄    | The D&F is a class D&F |
| df₅    | The class D&F includes an expiration date |
| df₆    | The D&F identifies the agency |
| df₇    | The D&F cites the relevant authority |
| df₈    | The D&F contains factual findings |
| df₉    | The D&F is signed by the authorized official |

---

## Phase 1: Propositional Logic

All formulas below are well-formed formulas (WFFs) in propositional logic. Formulas marked [schema] hold for any instantiation of the relevant atomic propositions.

### Subpart 1.1: Framework and Guiding Principles

**1. System Definition**

    s ↔ (f ∧ a ∧ g)

The system is established if and only if all three components are present.

**2. Exclusion of Internal Guidance**

    a → ¬ig

If agency regulations are part of the system, internal guidance is not.

**3. System Objectives**

    s → (m₁ ∧ m₂ ∧ m₃ ∧ m₄)

If the system is established, then it meets all four objectives.

**4. CO Authority**

    c → c_auth

If the actor is a CO, then the CO has authority to apply the rules.

**5. Permissive Innovation** [schema]

    (q₁ ∧ ¬q₂ ∧ ¬q₃) → q₄

If a strategy is in the government's best interest, is not addressed in the FAR, and is not prohibited, then it may be used.

**6. Risk Management**

    s → (m₅ ∧ ¬m₆)

If the system is established, then it focuses on risk management and does not eliminate all risk.

**7. Publication** [schema]

    r₁ → r₂

If a change to the FAR is proposed, then it is published in the Federal Register.

**8. Certifications**

    r₃ → r₄

If a certification is required, then that requirement must be authorized by statute. Equivalently: ¬r₄ → ¬r₃.

**9. Delegation** [schema]

    ¬d₂ → d₁

If delegation is not specifically prohibited, then the authority may be delegated. Note this captures the default-permissive posture of the rule. Contrapositive: ¬d₁ → d₂.

**10. Responsibility for Action** [schema]

    d₃ → c_resp

If a FAR section directs an action, the CO is responsible for that action.

**11. Regulatory Sunset** [schema]

    ¬u₁ → (u₂ ∨ u₃)

If a FAR section lacks a statutory basis, then it either expires after four years or is renewed by the FAR Council.

### Subpart 1.2: Agency Regulations

**12. Issuance Authority**

    a_iss → a

If the agency head issues a regulation, then agency regulations exist as part of the system. (This captures the permissive structure: agency heads may issue regulations.)

**13. Limitations on Agency Regulations**

    a_iss → ¬a_rep
    a_con → a_law

If an agency regulation is issued, it does not unnecessarily repeat the FAR. If an agency regulation conflicts with the FAR, then the conflict is required by law.

**14. Public Comment Requirement**

    (a_cost ∨ a_imp) → a_pub

If the regulation imposes significant cost or administrative impact, then it is published for public comment.

### Subpart 1.3: Deviations

**15. Authority to Deviate**

    v₂ → ¬v₁

If the deviation concerns CASB rules, then the agency does not deviate. Equivalently: v₁ → ¬v₂.

**16. Individual Deviations**

    (v₁ ∧ ¬v₅) → (v₃ ∧ v₄)

If the agency deviates and the deviation is not a class deviation, then the agency head authorizes it and the CO documents the justification.

**17. Class Deviations**

    v₅ → (v₆ ∧ v₇)

If the deviation is a class deviation, then the FAR Council approves it and the FAR Secretariat is notified.

**18. Treaties and Agreements**

    (v₁ ∧ v₈) → ¬v₉

If the agency deviates and the deviation is treaty-related, then the deviation is not inconsistent with post-treaty domestic law.

### Subpart 1.4: Authority and Responsibilities

**19. Exclusive Authority**

    c_sign ↔ c

A contract is signed if and only if the actor is a CO.

**20. CO Responsibilities (Pre-Signature)**

    c_sign → (c_legal ∧ c_funds ∧ c_fair)

If the CO signs the contract, then the CO has ensured legal compliance, funds availability, and fair treatment.

**21. Selection and Appointment**

    c → (c_appt ∧ c_ofpp)

If the actor is a CO, then the appointment was made in writing and is consistent with OFPP standards.

**22. Termination**

    c_term ∧ ¬c_retro

CO termination is in writing and is not retroactive. (These are conjunctive requirements.)

**23. Contracting Officer's Representative (COR)**

    cor_asgn → cor_des
    ¬cor_ffp → cor_asgn
    cor_ffp → (cor_asgn ∨ ¬cor_asgn)
    cor_asgn → (¬cor_del ∧ ¬cor_prc ∧ ¬cor_qty)

If a COR is assigned, the designation is in writing. If the contract is not firm-fixed-price, a COR is assigned. If the contract is firm-fixed-price, a COR may or may not be assigned (tautology, capturing permissiveness). If a COR is assigned, the COR does not delegate authority, change price, or change quality.

**24. Ratification Criteria**

    t₁ ↔ (t₂ ∧ t₃ ∧ t₄ ∧ t₅)

Ratification occurs if and only if all four conditions are met.

### Subpart 1.5: Determinations and Findings

**25. Definition**

    df₁ → (df₂ ∧ df₃)

If a D&F is executed, then it is a written approval and the findings support the determination.

**26. Class D&Fs**

    df₄ → df₅

If the D&F is a class D&F, then it includes an expiration date.

**27. Mandatory Content**

    df₁ → (df₆ ∧ df₇ ∧ df₈ ∧ df₉)

If a D&F is executed, then it identifies the agency, cites authority, contains findings, and is signed.

---

## Phase 2: Deontic Logic

The following reformulates each Phase 1 WFF by wrapping propositions or sub-formulas in deontic operators to capture the normative force of each rule. The propositional structure is preserved; only the modality is added.

Governing axiom: F(p) ↔ ¬P(p) and O(p) ↔ ¬P(¬p).

### Subpart 1.1: Framework and Guiding Principles

**1. System Definition**

    s ↔ (f ∧ a ∧ g)

No deontic operator. This is a definitional biconditional, not a norm.

**2. Exclusion of Internal Guidance**

    a → F(ig)

If agency regulations are part of the system, it is forbidden for internal guidance to be part of the system.

**3. System Objectives**

    s → (O(m₁) ∧ O(m₂) ∧ O(m₃) ∧ O(m₄))

If the system is established, then each objective is obligatory.

**4. CO Authority**

    c → O(c_auth)

If the actor is a CO, then it is obligatory that the CO has authority to apply the rules.

**5. Permissive Innovation** [schema]

    (q₁ ∧ ¬q₂ ∧ ¬q₃) → P(q₄)

If a strategy is in the best interest, not addressed in the FAR, and not prohibited, then using it is permitted.

**6. Risk Management**

    O(s → m₅) ∧ ¬O(m₆)

It is obligatory that the system focus on risk management. It is not obligatory to eliminate all risk.

**7. Publication** [schema]

    r₁ → O(r₂)

If a change to the FAR is proposed, then publication in the Federal Register is obligatory.

**8. Certifications**

    F(r₃ ∧ ¬r₄)

It is forbidden to require a certification unless the requirement is authorized by statute.

**9. Delegation** [schema]

    ¬d₂ → P(d₁)

If delegation is not specifically prohibited, then delegation is permitted.

**10. Responsibility for Action** [schema]

    d₃ → O(c_resp)

If a FAR section directs an action, the CO is obligated to be responsible for it.

**11. Regulatory Sunset** [schema]

    ¬u₁ → (O(u₂) ∨ P(u₃))

If a FAR section lacks a statutory basis, then expiration is obligatory unless renewal is permitted and exercised by the FAR Council.

### Subpart 1.2: Agency Regulations

**12. Issuance Authority**

    P(a_iss)

Issuance of agency regulations by the agency head is permitted.

**13. Limitations on Agency Regulations**

    a_iss → F(a_rep)
    a_con → O(a_law)

If an agency regulation is issued, unnecessary repetition is forbidden. If the regulation conflicts with the FAR, the conflict being required by law is obligatory. Equivalently: F(a_con ∧ ¬a_law).

**14. Public Comment Requirement**

    (a_cost ∨ a_imp) → O(a_pub)

If the regulation imposes significant cost or impact, then publication for comment is obligatory.

### Subpart 1.3: Deviations

**15. Authority to Deviate**

    P(v₁) ∧ F(v₁ ∧ v₂)

Deviation is permitted. Deviation from CASB rules is forbidden.

**16. Individual Deviations**

    (v₁ ∧ ¬v₅) → (P(v₃) ∧ O(v₄))

For an individual deviation, authorization by the agency head is permitted and documentation by the CO is obligatory.

**17. Class Deviations**

    v₅ → (O(v₆) ∧ O(v₇))

If the deviation is a class deviation, FAR Council approval and Secretariat notification are both obligatory.

**18. Treaties and Agreements**

    P(v₁ ∧ v₈) ∧ F(v₉)

Treaty-related deviation is permitted. Inconsistency with post-treaty domestic law is forbidden.

### Subpart 1.4: Authority and Responsibilities

**19. Exclusive Authority**

    O(c_sign → c) ∧ F(c_sign ∧ ¬c)

It is obligatory that only a CO signs a contract. It is forbidden for a non-CO to sign.

**20. CO Responsibilities (Pre-Signature)**

    c_sign → (O(c_legal) ∧ O(c_funds) ∧ O(c_fair))

If the CO signs the contract, then legal compliance, funds availability, and fair treatment are each obligatory.

**21. Selection and Appointment**

    c → (O(c_appt) ∧ O(c_ofpp))

If the actor is a CO, then written appointment and OFPP consistency are each obligatory.

**22. Termination**

    O(c_term) ∧ F(c_retro)

Written termination is obligatory. Retroactive termination is forbidden.

**23. Contracting Officer's Representative (COR)**

    cor_asgn → O(cor_des)
    ¬cor_ffp → O(cor_asgn)
    cor_ffp → P(cor_asgn)
    cor_asgn → (F(cor_del) ∧ F(cor_prc) ∧ F(cor_qty))

If a COR is assigned, written designation is obligatory. If the contract is not FFP, COR assignment is obligatory. If the contract is FFP, COR assignment is permitted. If a COR is assigned, delegation, price changes, and quality changes are each forbidden.

**24. Ratification Criteria**

    P(t₁) ↔ (t₂ ∧ t₃ ∧ t₄ ∧ t₅)

Ratification is permitted if and only if all four conditions are satisfied.

### Subpart 1.5: Determinations and Findings

**25. Definition**

    df₁ → (O(df₂) ∧ O(df₃))

If a D&F is executed, then written approval and supporting findings are each obligatory.

**26. Class D&Fs**

    P(df₄) ∧ (df₄ → O(df₅))

Class D&Fs are permitted. If a D&F is a class D&F, an expiration date is obligatory.

**27. Mandatory Content**

    df₁ → (O(df₆) ∧ O(df₇) ∧ O(df₈) ∧ O(df₉))

If a D&F is executed, then agency identification, citation, findings, and signature are each obligatory.

---

## Notes on Expressiveness Limits

Three limitations of this formalization are worth noting:

First, propositional logic cannot express true universality. Statements marked [schema] would require first-order predicate logic with universal quantifiers to formalize completely. The propositional versions hold for any specific instantiation but do not formally assert that they hold for all instances.

Second, the deontic operators used here follow Standard Deontic Logic (SDL). SDL has known paradoxes (Ross's paradox, the Good Samaritan paradox, contrary-to-duty obligations) that may become relevant in more complex regulatory interactions. A production system would likely need a non-monotonic or defeasible deontic logic.

Third, temporal and conditional obligation structures ("shall, within 30 days...") are flattened into simple obligations here. A full formalization of procedural deadlines would require temporal deontic logic (e.g., combining SDL with Linear Temporal Logic).

