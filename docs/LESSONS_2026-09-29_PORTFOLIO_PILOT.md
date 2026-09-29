# Session Lessons — Portfolio Pilot / Research Mesh

Updated: 2026-09-29 JST  
Status: Reusable operating knowledge  
Scope: AI Business Transformation / portfolio program / Research Mesh handoff

## Purpose

This document records conclusions that are reusable beyond the immediate task history.

It is not a status record. Current repository state, deployment state, Research Mesh state, and open work must always be fresh-read from their canonical sources.

---

## 1. Treat the four sites as one portfolio program, but keep one active theme

A multi-site portfolio can show different capabilities without forcing every site to explain everything.

Current role split:

- AI Business Transformation: Consulting / Thinking
- Kaigo Rules: Domain / Operations
- Parenting Evidence: Research / Evidence
- Studio Lab Research: AI Engineering / Experimentation

The useful operating rule is:

> Keep the portfolio multi-dimensional, but keep the active build/research theme narrow.

Working on all four sites in parallel makes it harder to tell whether delays or quality problems come from the subject matter, the workflow, or the Research Mesh itself.

A single active theme improves attribution, convergence, and review quality.

---

## 2. A portfolio should demonstrate a repeatable capability, not just count projects

Four finished websites are not automatically stronger than one or two sites with strong evidence.

The transferable capability to demonstrate is closer to:

> Identify a difficult operational problem, reconstruct the constraints and evidence, compare implementation options, design controls, implement a bounded solution, and verify it.

Therefore the highest-value content is not generic profile copy or visual polish.

The strongest evidence is a case that shows:

- the original operational problem;
- constraints and failure impact;
- evidence used;
- decisions and trade-offs;
- what was automated and what remained human;
- verification and stop conditions;
- failures and revisions;
- what can and cannot be generalized.

This structure should be reused across the portfolio.

---

## 3. Convert domain experience into decision criteria

Domain experience becomes more valuable when it is translated from biography into reusable reasoning.

Example:

Weak form:

> VBAで業務を自動化した。

Stronger form:

> 定型性、例外率、変更頻度、説明責任を踏まえると、生成AIではなく従来型自動化を選ぶ方が適切な条件は何か。

Likewise, Kaigo Rules should not be presented only as a care-regulation project.

It can demonstrate general lessons about:

- source-of-truth design;
- regulatory change management;
- evidence traceability;
- machine validation;
- independent verification;
- human review;
- handling UNKNOWN / HOLD;
- preventing unsupported confidence.

This translation from experience to decision criteria is a core differentiator for the portfolio.

---

## 4. Build evidence-bearing case studies before adding more presentation layers

The first site foundation was useful because it created a visible shell quickly.

However, once the positioning is understandable, additional visual refinement has lower marginal value than adding one strong case study.

Recommended order:

1. establish a clear positioning shell;
2. produce one evidence-bearing case;
3. test whether the case demonstrates the intended capability;
4. then refine navigation, design, and additional content.

Do not continue polishing an empty shell.

For AI Business Transformation, the first strong candidate remains:

> 複雑な制度文書をAIで扱うとき、正確性をどう担保するか

using Kaigo Rules as the case base.

---

## 5. Keep implementation simple until the content model requires complexity

The initial public site was implemented as static HTML/CSS.

That was sufficient to validate:

- positioning;
- information hierarchy;
- visual direction;
- mobile readability;
- Vercel publication;
- links to evidence projects.

There is no benefit in adopting a heavier framework merely to appear more technically sophisticated.

A framework migration should be triggered by a concrete requirement such as:

- many repeated content pages;
- structured content generation;
- search;
- dynamic filtering;
- reusable components whose maintenance cost is material;
- APIs or interactive tools;
- authentication or user state.

Until then, simple architecture reduces failure modes and keeps attention on the quality of the evidence.

---

## 6. Commit, merge, and release are different state transitions

One of the clearest operational lessons from this session is:

> A source change is not the same thing as a publication decision.

Automatic deployment couples two different decisions:

1. Is this change worth preserving in the repository?
2. Is this exact repository state ready to replace the public production site?

Those decisions often occur at different times.

For this portfolio, the safer default is:

```
work
→ verify
→ commit / merge
→ deployment decision
→ HOLD by default
→ manual production deploy only when justified
→ verify production
```

This is useful beyond Vercel. It is a general release-management principle.

The current repository operationalizes this with:

`deployment_decision: DEPLOY | HOLD`

and defaults to `HOLD`.

---

## 7. Release gates should be based on publishability, not activity

A deployment should not occur because:

- a task finished;
- a commit exists;
- a pull request merged;
- an agent produced a result.

The relevant question is:

> Is the exact current state coherent enough, useful enough, and verified enough to become the public version?

A practical release gate includes:

- material public value;
- coherent scope;
- no known blocking WIP;
- identifiable exact commit;
- ability to verify production after release.

This prevents high task throughput from turning into high public churn.

---

## 8. Fail-closed behavior is evidence of system maturity, but repeated meta-repair has diminishing returns

Research Mesh produced useful evidence by rejecting retry-policy proposals rather than promoting them.

A failed proposal can be a positive system result when:

- the failure is detected before activation;
- the counterexample is durable;
- the broader question remains correctly unresolved;
- production and policy boundaries are preserved.

However, successive protocol repairs can become an optimization loop with falling external value.

A warning sign is:

```
V1 FAIL
→ V2 fixes V1
→ V2 FAIL
→ V3 fixes V2
→ V3 FAIL
→ V4 fixes V3
→ ...
```

Even when each step is intellectually valid, the system may be spending most of its effort on itself.

The correct response is not necessarily to weaken verification.

It may be to bound the unresolved question, preserve HOLD, and redirect the system to an external useful task.

---

## 9. External work is a stronger acceptance test than more self-analysis

Research Mesh should increasingly be judged on whether it can produce useful work outside its own architecture.

A strong acceptance test is an external topic where:

- evidence is available;
- claims can be challenged;
- output has practical value;
- bounded conclusions are possible;
- the user can inspect the final artifact.

The Portfolio Pilot is therefore not only portfolio production.

It is also a test of whether Research Mesh can:

- formulate useful questions;
- gather and preserve evidence;
- generate counterevidence;
- converge on a usable result;
- avoid incorrect promotion;
- avoid endless self-referential work;
- require human intervention only at real boundaries.

This is a stronger maturity signal than another internal protocol proposal.

---

## 10. Preserve uncertainty instead of forcing completion

For research and portfolio case studies, unresolved findings should remain visibly unresolved.

Good states include:

- VERIFIED
- NOT SUPPORTED
- HOLD
- UNKNOWN
- bounded negative result

A portfolio does not become weaker because it documents a failed hypothesis or unresolved infrastructure limit.

For complex AI/DX work, showing why a conclusion was not justified can demonstrate better judgment than showing only successful outputs.

Do not convert uncertainty into confident narrative merely for presentation.

---

## 11. The most useful portfolio cases expose operational friction

A polished success story often hides the part that is most transferable.

The useful questions are:

- What failed?
- What assumption was wrong?
- What did the first design miss?
- What could not be verified?
- What did the system do when evidence was incomplete?
- Where did human judgment remain necessary?
- What became deterministic after the failure?
- What boundary was deliberately not crossed?

This makes Kaigo Rules and Studio Lab valuable not despite their failures and HOLD states, but partly because those events reveal real implementation constraints.

---

## 12. Reusable case-study structure

For future portfolio work, use this as a default structure rather than inventing a new format for every project.

### A. Decision

What decision did the organization or operator actually need to make?

### B. Constraints

What made the problem hard?

Examples:
- regulatory requirements;
- accuracy;
- incomplete inputs;
- frequent change;
- auditability;
- security;
- human capacity;
- legacy tools.

### C. Baseline

How was the work performed before the intervention?

### D. Options

What were the realistic alternatives?

Examples:
- manual work;
- standardization;
- Excel / VBA / Power Query;
- deterministic software;
- LLM assistance;
- agentic workflow;
- external vendor.

### E. Design

What was changed, and why?

### F. Control model

Where were:
- validation;
- human review;
- immutable evidence;
- rollback;
- stop conditions;
- permission boundaries?

### G. Evidence

What evidence supports the result?

Distinguish:
- observed;
- inferred;
- externally supported;
- unverified.

### H. Failure / counterevidence

What did not work or what contradicted the initial design?

### I. Result

What was actually established?

Avoid claiming beyond the evidence.

### J. Generalization

Under what conditions would the lesson transfer to another organization?

### K. Limits

Where should it not be generalized?

---

## 13. Cross-project operating principle

The combined lesson is:

> Optimize for trustworthy useful output, not activity, sophistication, or automation rate.

This implies:

- one active theme at a time;
- evidence before polish;
- simple architecture until complexity earns its cost;
- verification before promotion;
- merge separated from release;
- uncertainty preserved;
- internal optimization bounded;
- external usefulness used as the final test.

These principles are intended to be reused across the four portfolio sites and future Research Mesh work.

---

## Deployment decision for this knowledge record

`deployment_decision: HOLD`

Reason:

This is internal reusable operating knowledge. It should be versioned in the repository but does not change the public-facing site and therefore should not trigger a production deployment.
