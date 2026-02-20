# Revolutionary FAR Overhaul (RFO) -- Propositional Logic Dataset

A systematic formalization of the Federal Acquisition Regulation (FAR) into classical propositional logic. Each FAR section is decomposed into atomic propositions, mapped to formal logic statements, validated for soundness, and exported as structured CSV data.

No one has done this before at this level of granularity. The goal is to make federal procurement regulations machine-readable, queryable, and suitable for automated compliance checking, dependency analysis, and decision support tooling.

A common objection to applying propositional logic to the FAR is that the regulation is written in a procedural format rather than a declarative one, making direct formalization non-trivial. Natural language ambiguity and the context-dependent meaning of regulatory terms resist straightforward translation into formal expressions. However, propositional logic serves as a practical and methodologically sound foundation for this work. Once all extracted propositions have been manually validated for accuracy and structural integrity, the roadmap calls for extending the data structure to incorporate deontic logic, which is purpose-built to capture the normative character of regulatory text by explicitly representing the obligations, permissions, and prohibitions that form the backbone of FAR language.


## What This Is

The FAR is the primary regulation governing federal procurement in the United States. It runs roughly 2,000 pages of dense legal text covering everything from competition requirements to contract cost accounting to labor standards. This project converts that text into formal propositional logic using five classical operators:

- Conjunction (AND, symbol: ^) -- "both X and Y are required"
- Disjunction (OR, symbol: v) -- "either X or Y satisfies"
- Negation (NOT, symbol: ~) -- "X shall not occur"
- Material implication (IF...THEN, symbol: ->) -- "if condition X, then requirement Y"
- Biconditional (IFF, symbol: <->) -- "X if and only if Y"

Each proposition is traced back to its exact FAR section, decomposed into atomic components, assigned formal logic, tagged with justification rules from a standardized 18-rule set, and independently validated against both logical soundness and real-world regulatory sense.

## CSV Schema

Every output file uses this 13-column structure:

| Column | Type | Description |
|--------|------|-------------|
| RFO_Part | Integer | FAR part number |
| Section_Number | String | Original FAR section reference (e.g., 7.105(a)(1)) |
| Propositional_ID | String | Unique identifier (e.g., P_7_105_a_1) |
| Natural_Language | String | Complete regulatory text, word-for-word from source |
| Atomic_Propositions | String | Semicolon-delimited atomic components with sub-IDs |
| Formal_Logic_Statement | String | Propositional logic formula |
| Dependencies | String | Cross-referenced proposition IDs, or "None" |
| Justification_Rules | String | Logic rules applied, with rule numbers |
| Validation_Status | Enum | VALIDATED, PENDING_REVIEW, REJECTED, or INCOMPLETE |
| Logical_Check | Enum | PASS or FAIL |
| Real_World_Check | Enum | PASS or FAIL |
| Validation_Notes | String | Explanation of validation outcome and flagged issues |
| Confidence_Level | Enum | HIGH, MEDIUM, or LOW |

## File Naming Convention

All data files follow the pattern `RFO_Part_[N]_Propositional_Logic.csv` where N is the FAR part number.

## Methodology

Extraction follows a 5-phase pipeline defined in `Text_to_Logic_Prompt_v3_0_iterative.md`:

1. **Assess and Plan** -- Measure input size, classify complexity, identify segment boundaries, build a processing map.
2. **Build the Skeleton** -- Scan source text for every section and subsection. Assign propositional IDs. Apply the parent proposition rule (any section with subsections gets a parent entry). The skeleton becomes the single source of truth for all IDs.
3. **Extract Segments** -- For each segment: copy regulatory text verbatim, decompose into atomic propositions, construct formal logic statements, document justification rules, run soundness validation (logical check + real-world check), assign confidence levels. Segments are processed sequentially and exported independently.
4. **Merge and Resolve Dependencies** -- Combine all segment CSVs. Resolve cross-references (replace DEFERRED markers with actual proposition IDs). Build cross-part dependency maps.
5. **Audit and Finalize** -- Structural checks (ID uniqueness, parent-child integrity, no gaps). Content checks (operator validity, dependency resolution, no blank fields). Consistency checks (validation status matches outcomes, HIGH-RISK rules flagged).

### Justification Rules

The project uses 18 standard rules of propositional logic. Three are flagged HIGH-RISK due to their potential to alter regulatory meaning if applied incorrectly:

- Rule 9 (Simplification) -- can drop required conjuncts
- Rule 12 (Commutation) -- can obscure regulatory priority
- Rule 15 (Material Implication) -- can reverse causality

Any proposition using a HIGH-RISK rule is automatically set to PENDING_REVIEW with a MEDIUM confidence floor, regardless of other validation outcomes.

### Key Design Decisions

**Word-for-word accuracy.** The Natural_Language column preserves the exact FAR text. No paraphrasing. In regulatory contexts, even minor rewording introduces unacceptable risk of meaning drift.

**No self-validation.** The same model that generates propositions should not be the sole validator. All extractions are marked PENDING_REVIEW until independently reviewed. The dataset includes a self-validation warning on every final export.

**"May" is not "shall."** Permissive language ("the contracting officer may") is modeled as a tautology in the consequent: `Condition -> (Action v ~Action)`. This preserves the discretionary nature without converting permission into obligation.

**Dependencies are resolved separately.** During initial extraction, all cross-references are marked DEFERRED. Resolution happens in a dedicated merge phase to prevent cascading errors during segment processing.

## Known Limitations

**Validation is incomplete.** 39% of propositions are still PENDING_REVIEW. These require independent human review, not just model re-checking. The VALIDATED status means the proposition passed automated logical and real-world checks, not that it has been independently audited.

**Encoding artifacts.** Some files contain UTF-8 multi-byte encoding artifacts in the Formal_Logic_Statement column (visible as mojibake for logical operators). The logical structure is correct but the display characters need cleanup in those rows.

**CSV parsing issues.** Parts 12 and 15 have known issues with embedded newlines in the Natural_Language column that can break naive CSV parsers. Use a proper CSV library (Python csv module, pandas, etc.) rather than line-splitting.

**Context window degradation.** Extraction quality can degrade in rows 80+ of a single processing pass due to LLM context window limitations. The methodology mitigates this through segmented processing, but earlier extractions (before the iterative methodology was adopted) may have more issues in their latter halves.

**Propositional logic constraints.** Classical propositional logic cannot fully capture deontic modality (obligations vs. permissions vs. prohibitions), temporal relationships, or quantified statements. The dataset approximates these using the available operators and documents the approximations in Validation_Notes.

## Potential Applications

- Automated compliance checking against FAR requirements
- Dependency network analysis across FAR parts
- Decision support tools for contracting officers
- Regulatory change impact analysis
- Training data for legal/regulatory AI systems
- Foundation layer for an architecture combining propositional logic with deontic logic and natural language interfaces

## License

CC BY-NC 4.0 (Creative Commons Attribution-NonCommercial 4.0 International). Free for non-commercial use with attribution.

## Tools Used

- **Extraction:** Claude (Anthropic) with structured methodology prompts
- **Source data:** FAR MHT files, HTML-parsed
- **Output format:** CSV (UTF-8)
- **Methodology version:** Text_to_Logic_Prompt_v3_0_iterative.md
