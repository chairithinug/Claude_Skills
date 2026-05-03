# Graph Report - .  (2026-05-03)

## Corpus Check
- Corpus is ~36,475 words - fits in a single context window. You may not need a graph.

## Summary
- 72 nodes · 78 edges · 10 communities detected
- Extraction: 83% EXTRACTED · 17% INFERRED · 0% AMBIGUOUS · INFERRED: 13 edges (avg confidence: 0.73)
- Token cost: 150,070 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Core Skills & Reasoning|Core Skills & Reasoning]]
- [[_COMMUNITY_Fortune & Divination Traditions|Fortune & Divination Traditions]]
- [[_COMMUNITY_Interview Competency Framework|Interview Competency Framework]]
- [[_COMMUNITY_Research Methodology|Research Methodology]]
- [[_COMMUNITY_User Support Companion|User Support Companion]]
- [[_COMMUNITY_Governance & Standards|Governance & Standards]]
- [[_COMMUNITY_Token Optimization Patterns|Token Optimization Patterns]]
- [[_COMMUNITY_Executive Multi-Lens Analysis|Executive Multi-Lens Analysis]]
- [[_COMMUNITY_Skill Patterns & Conventions|Skill Patterns & Conventions]]
- [[_COMMUNITY_Strategic Decision-Making|Strategic Decision-Making]]

## God Nodes (most connected - your core abstractions)
1. `Skill Authoring Standards` - 14 edges
2. `Claude_Skills Repository` - 10 edges
3. `Executive Lensing Skill` - 9 edges
4. `Deciding Skill` - 7 edges
5. `Multi-Tradition Divination` - 6 edges
6. `Researching Topics Skill` - 5 edges
7. `Talking It Out Skill` - 5 edges
8. `Token Optimizing Skill` - 4 edges
9. `Skill Chaining Pattern` - 4 edges
10. `Fortune Telling Skill` - 4 edges

## Surprising Connections (you probably didn't know these)
- `Devil Advocating Skill` --semantically_similar_to--> `Working Through Skill`  [INFERRED] [semantically similar]
  devil-advocating/SKILL.md → working-through/SKILL.md
- `Researching Topics Skill` --semantically_similar_to--> `Devil Advocating Skill`  [INFERRED] [semantically similar]
  researching-topics/SKILL.md → devil-advocating/SKILL.md
- `Talking It Out Skill` --semantically_similar_to--> `Working Through Skill`  [INFERRED] [semantically similar]
  talking-it-out/SKILL.md → working-through/SKILL.md
- `Executive Lensing Skill` --conceptually_related_to--> `Deciding Skill`  [INFERRED]
  executive-lensing/evals/loops/2026-05-03/baseline-description.txt → deciding/SKILL.md
- `AI Fluency Planning Skill` --conceptually_related_to--> `Deciding Skill`  [INFERRED]
  ai-fluency-planning/SKILL.md → deciding/SKILL.md

## Hyperedges (group relationships)
- **Skill Authoring Workflow** — eval_first_principle, template_evals_md, template_skill_md, canonical_section_structure, standards_authoring_standard [EXTRACTED 0.95]
- **Skill Discovery and Loading Mechanism** — frontmatter_discovery, progressive_disclosure_pattern, skill_naming_convention, reference_depth_rule [INFERRED 0.85]
- **Skill Safety and Governance** — no_secrets_rule, html_demo_safety_contract, anthropic_docs_precedence, load_bearing_content_preservation [INFERRED 0.85]
- **Reasoning Skill Family (Decision & Analysis)** — deciding_skill, executive_lensing_skill, negotiating_skill, skill_chaining_pattern [INFERRED 0.80]
- **Executive Suite Multi-Lens Analysis** — executive_lensing_ceo_lens, executive_lensing_cfo_lens, executive_lensing_coo_lens, executive_lensing_cmo_lens, executive_lensing_cto_lens, executive_lensing_chro_lens [EXTRACTED 1.00]
- **Multi-Tradition Divination System** — fortune_telling_rokuyo, fortune_telling_chinese, fortune_telling_western, fortune_telling_thai, fortune_telling_vedic [EXTRACTED 1.00]
- **Interview Process Workflow** — interviewing_interviewee_prep, interviewing_interviewer_design, interviewing_interview_debrief [EXTRACTED 1.00]
- **User Support Spectrum Skills** — talking_it_out_skill, working_through_skill, devil_advocating_skill, researching_topics_skill [INFERRED 0.75]

## Communities (10 total, 3 thin omitted)

### Community 0 - "Core Skills & Reasoning"
Cohesion: 0.15
Nodes (16): Anthropic Docs Precedence Rule, SKILL.md Body Line Limit (500 lines), Canonical Four-Section Structure, Project Instructions, Eval-First Principle, Frontmatter as Discovery Surface, HTML Demo Public-GitHub Safety Contract, Long-Skill Variant (Step N headings) (+8 more)

### Community 1 - "Fortune & Divination Traditions"
Cohesion: 0.14
Nodes (14): Red-Team Steelman Opposition Argument, Devil Advocating Skill, Compare-Options Mode, Deep-Dive Mode, Forced Methodology for Topic Research, Quick-Scan Mode, Researching Topics Skill, Companion for Hard Times (+6 more)

### Community 2 - "Interview Competency Framework"
Cohesion: 0.31
Nodes (10): AI Fluency Planning Skill, Decision Framework Reference, Deciding Skill, Explaining Skill, Negotiating Skill, Quick Answering Skill, Claude_Skills Repository, Skill Chaining Pattern (+2 more)

### Community 3 - "Research Methodology"
Cohesion: 0.2
Nodes (10): Auspicious Timing Mode, Chinese BaZi and Zodiac, Daily Luck Overview Mode, Multi-Tradition Divination, Japanese Rokuyo, Fortune Telling Skill, Specific Question Mode, Thai Day-of-Week Astrology (+2 more)

### Community 4 - "User Support Companion"
Cohesion: 0.25
Nodes (8): Interview Debrief Reference, Interviewee Prep Reference, Interviewer Design Reference, Competency-Based Interview Backbone, Interview Debrief Mode, Interviewee Prep Mode, Interviewer Design Mode, Interviewing Skill

### Community 5 - "Governance & Standards"
Cohesion: 0.29
Nodes (7): CEO Lens — Strategy & Optionality, CFO Lens — Capital & Financial Risk, CHRO Lens — People & Culture, CMO Lens — Market & Brand, COO Lens — Execution & Operations, CTO Lens — Technology & Architecture, Executive Lensing Skill

### Community 6 - "Token Optimization Patterns"
Cohesion: 0.67
Nodes (4): Load-Bearing Content Preservation Principle, Token Optimizing Quality Eval, Token Optimizing Skill, Token Optimizing Worked Example

## Knowledge Gaps
- **40 isolated node(s):** `Evaluation Template`, `Loop Results Template`, `Decision Framework Reference`, `Token Optimizing Quality Eval`, `SKILL.md Body Line Limit (500 lines)` (+35 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **3 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Claude_Skills Repository` connect `Interview Competency Framework` to `Core Skills & Reasoning`, `Governance & Standards`, `Token Optimization Patterns`?**
  _High betweenness centrality (0.164) - this node is a cross-community bridge._
- **Why does `Skill Authoring Standards` connect `Core Skills & Reasoning` to `Interview Competency Framework`?**
  _High betweenness centrality (0.145) - this node is a cross-community bridge._
- **Why does `Executive Lensing Skill` connect `Governance & Standards` to `Interview Competency Framework`?**
  _High betweenness centrality (0.080) - this node is a cross-community bridge._
- **Are the 4 inferred relationships involving `Deciding Skill` (e.g. with `Executive Lensing Skill` and `Negotiating Skill`) actually correct?**
  _`Deciding Skill` has 4 INFERRED edges - model-reasoned connections that need verification._
- **What connects `Evaluation Template`, `Loop Results Template`, `Decision Framework Reference` to the rest of the system?**
  _40 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Fortune & Divination Traditions` be split into smaller, more focused modules?**
  _Cohesion score 0.14 - nodes in this community are weakly interconnected._