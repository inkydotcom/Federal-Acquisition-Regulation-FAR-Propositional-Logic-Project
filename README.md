# Federal Acquisition Regulation (FAR) Propositional Logic Project

## Overview

This project converts the Federal Acquisition Regulation (FAR) into formal propositional logic statements. The goal is to transform complex regulatory prose into structured logical representations that support automated analysis, dependency mapping, and validation of federal procurement requirements.

The project is currently mapping the RFO model deviation text, converting its regulatory framework into structured propositional logic. Future work will extend this same methodology to agency acquisition regulation supplements.

## Why This Matters

Federal procurement regulations are dense, interconnected, and often ambiguous. Converting them to formal logic enables:

- **Automated compliance checking**: Verify whether a procurement approach satisfies all applicable requirements
- **Dependency mapping**: Identify which regulations affect each other and trace impact of proposed changes
- **Logical consistency validation**: Find contradictions, gaps, and circular dependencies in the regulations
- **Machine-readable requirements**: Enable software tools to parse and apply procurement rules systematically

## Methodology

The conversion follows an 8-step pipeline:

1. **HTML Extraction**: Parse RFO parts from MHT source files
2. **Content Parsing**: Extract regulatory text while excluding headers, navigation, and metadata
3. **Atomic Proposition Identification**: Break down complex statements into discrete logical units
4. **Formal Logic Statement Creation**: Apply standard logical operators (∧, ∨, ⊃, ~, ≡)
5. **Cross-Reference Mapping**: Track dependencies between regulatory sections
6. **Validation Execution**: Check logical consistency and real-world applicability
7. **Confidence Assessment**: Rate reliability of each formalization
8. **CSV Output Generation**: Store structured data in standardized format

### Core Principle: Word-for-Word Accuracy

Every substantive word from source documents must appear in the final output. Paraphrasing introduces unacceptable risk of meaning drift in regulatory contexts. Comprehensive audits verify complete coverage of source material.

## Current Status

### Completed Parts (RFO Model Deviation Text)

- **Part 1**: Federal Acquisition Regulations System (68 propositions)
- **Part 5**: Publicizing Contract Actions (38 propositions)
- **Part 6**: Competition Requirements (57 propositions)
- **Part 7**: Acquisition Planning (63 propositions)
- **Part 12**: Acquisition of Commercial Products and Services (1,273 propositions)
- **Part 15**: Contracting by Negotiation (326 propositions)
- **Part 16**: Types of Contracts (111 propositions)
- **Part 19**: Small Business Programs (77 propositions)
- **Part 26**: Other Socioeconomic Programs (28 propositions)
- **Part 33**: Protests, Disputes, and Appeals (111 propositions)

**Total**: 2,152 propositions across 10 RFO parts

### Project Scope

With 10 of 53 RFO parts formalized (19% of parts), this represents substantial coverage of critical procurement domains:
- **Foundation regulations**: Parts 1, 5, 6 (System framework, publicity, competition)
- **Contract formation**: Parts 12, 15, 16 (Commercial acquisition, negotiation, contract types)
- **Planning and socioeconomic**: Parts 7, 19, 26 (Acquisition planning, small business, other programs)
- **Administration**: Part 33 (Protests, disputes, appeals)

The completed parts include many of the most frequently referenced sections in federal procurement practice.

**Part 52 Reference File**: Part 52 (Solicitation Provisions and Contract Clauses) is maintained as a complete reference file in the project but does not require propositional logic formalization at this time.

**Future Expansion**: Following completion of the RFO base regulation, the same methodology will be applied to agency acquisition regulation supplements (DFARS, HHSAR, and others), creating a comprehensive logical framework for the entire federal acquisition regulatory system.

### Dependency Analysis

- Extensive internal connections between completed parts identified
- Part 52 available as complete reference file for clause cross-references
- Comprehensive cross-reference mapping across the 10 formalized parts
- Known circular dependencies exist in Part 5 presolicitation requirements (bidirectional cross-references confirmed in source)
- Ongoing validation of medium-confidence entries across complex conditional sections

## Data Structure

Each proposition record includes:

| Field | Description |
|-------|-------------|
| RFO_Part | RFO part number (integer) |
| Section_Number | RFO section identifier |
| Propositional_ID | Unique ID in format P_[Part]_[Section]_[Subsection] |
| Natural_Language | Original regulatory text |
| Atomic_Propositions | Component logical statements |
| Formal_Logic_Statement | Formalized expression using logical operators |
| Dependencies | References to related proposition IDs |
| Justification_Rules | Logical rules applied (from 18 standard rules) |
| Validation_Status | Validated/Pending/Needs Review |
| Logical_Check | Pass/Fail for internal consistency |
| Real_World_Check | Pass/Fail for practical applicability |
| Validation_Notes | Comments on edge cases or uncertainties |
| Confidence_Level | High/Medium/Low reliability rating |

### Logical Operators

- ∧ (conjunction): AND
- ∨ (disjunction): OR
- ⊃ (material implication): IF-THEN
- ~ (negation): NOT
- ≡ (material equivalence): IF AND ONLY IF

## File Organization

```
RFO_Part_[X]_Propositional_Logic.csv - Formalized propositions for each RFO part
RFO_far_part_52_provisions_clauses.csv - Reference file (different format, complete)
README.md - This file
```

## Known Issues

1. **Medium Confidence Entries**: Complex compound sections across multiple parts need independent validation
2. **Circular Dependencies**: Part 5 contains bidirectional cross-references (confirmed as legitimate in source)
3. **Validation Status**: Most propositions marked "PENDING_REVIEW" - require independent expert validation to upgrade confidence levels
4. **Part 52 Formalization**: While Part 52 exists as a complete reference file, it has not been formalized into propositional logic, creating gaps in dependency resolution for clauses referenced by other parts
5. **Coverage Gaps**: Several RFO parts remain incomplete (Parts 2, 3, 4, 8-11, 13-14, 17-18, 20-25, 27-32, 34-51)

## Next Steps

### Short-Term (Current RFO Work)

1. **Independent Validation**: Recruit domain experts to validate medium and low-confidence propositions
2. **Dependency Network Analysis**: Run comprehensive cross-reference analysis across all 10 completed RFO parts
3. **Strategic Expansion**: Prioritize remaining RFO parts based on:
   - Reference frequency from completed parts
   - Critical procurement process stages
   - Regulatory impact and usage patterns
4. **Quality Assurance**: Conduct systematic audits for word-for-word accuracy across all completed parts
5. **Tool Development**: Build automated compliance checking tools using the formalized logic

### Long-Term (Future Expansion)

6. **Agency Supplements**: Apply the same propositional logic methodology to agency acquisition regulation supplements (e.g., DFARS, HHSAR, AIDAR, etc.)
7. **Cross-System Dependencies**: Map logical dependencies between RFO and agency-specific regulations
8. **Complete Coverage**: Achieve comprehensive formalization across the entire federal acquisition regulatory framework

## Technical Details

### ID Management System

The format P_[Part]_[Section]_[Subsection] ensures:
- Unique identification across all RFO parts
- Preservation of regulatory structure
- Prevention of namespace conflicts as project scales

### Validation Layers

1. **Logical Consistency**: Automated checks for contradictions and tautologies
2. **Real-World Applicability**: Manual review against actual procurement scenarios
3. **Confidence Scoring**: High (straightforward), Medium (complex conditionals), Low (ambiguous language)

### 18 Standard Rules of Propositional Logic

Foundation for all formalizations:
- Modus Ponens, Modus Tollens
- Hypothetical Syllogism, Disjunctive Syllogism
- Conjunction, Simplification, Addition
- De Morgan's Laws, Distribution, Association
- Commutation, Idempotence, Absorption
- Double Negation, Contraposition, Implication
- Exportation, Tautology

## Tools and Resources

- **Python**: HTML parsing and logic extraction scripts
- **CSV**: Structured data storage format
- **React**: Interactive dependency visualization
- **Unicode**: Standardized logical notation (∧, ∨, ⊃, ~, ≡)
- **MHT files**: Source RFO regulatory documents

## Contributing

When adding new formalizations:

1. Follow the 8-step pipeline exactly
2. Maintain word-for-word accuracy through audit passes
3. Use consistent ID format: P_[Part]_[Section]_[Subsection]
4. Document all dependencies and cross-references
5. Complete multi-layer validation before marking as high confidence
6. Update dependency maps when adding new sections

### Contributor Recognition

Major contributors to this project will be recognized for their substantive work. Those who make significant contributions to the formalization effort (completing multiple parts, developing critical tools, or providing expert validation) will be offered opportunities to share in any future commercial applications or derivative works that may emerge from this project.

This project currently operates under CC BY-NC 4.0 (non-commercial), but significant contributors will have the opportunity to participate in future value creation should commercial opportunities arise.

## Key Learnings

- **Accuracy over elegance**: Regulatory precision trumps concise formalization
- **Systematic ID management**: Prevents chaos as project scales
- **Multi-layered validation**: No single check catches all issues
- **Dependency tracking**: Reveals regulatory networks and critical hubs
- **Iterative refinement**: First pass captures 80%, subsequent passes catch edge cases

## License

This work is licensed under **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)**.

This license restricts the use of this work to non-commercial purposes only. You are free to share and adapt the material, provided you give appropriate credit and do not use it for commercial purposes.

The source material consists of public domain U.S. federal regulations.
