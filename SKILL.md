---
name: phd-paper-analysis
description: Produce an exhaustive PhD-level Traditional Chinese HTML report for exactly one academic paper from a PDF, uploaded file, URL, DOI, arXiv ID, citation, or exact title. Use when the user asks for deep academic paper analysis, formula-by-formula explanation, architecture/figure interpretation, experimental and ablation critique, reproducibility review, or audio deepfake detection relevance for a single paper.
---

# PhD Paper Analysis

## Core Rule

Analyze exactly one paper and produce an exhaustive Traditional Chinese HTML research report.

Keep the workflow scoped to:

```text
one paper -> verified identity -> full-paper reading -> PhD-level Traditional Chinese HTML report
```

Do not schedule tasks, create reminders, manage recurring routines, or turn the answer into a broad literature review unless the user explicitly asks for that separately.

## Input Handling

Accept exactly one paper from:

- PDF or uploaded file
- URL
- DOI
- arXiv ID
- exact title
- citation

If the user provides multiple papers, ask whether to analyze only the first paper or create separate runs. If no paper is provided, ask for the paper unless the user explicitly asks Codex to choose one.

For DOI, arXiv ID, URL, title, or citation inputs, resolve the paper through primary or authoritative sources where possible, such as the publisher page, arXiv, proceedings page, OpenReview, PubMed, ACL Anthology, IEEE, ACM, Springer, or the authors' official project page.

## Identity Verification

Before analysis, verify and report the paper identity:

- title
- authors
- venue or source
- publication year
- DOI, arXiv ID, URL, or local file path

If the paper cannot be accessed, say so clearly and do not invent details. If only metadata or abstract access is available, explain that limitation and avoid presenting unavailable sections as read.

## Reading Scope

Read the entire available paper carefully, including:

- abstract
- introduction
- related work
- method
- experiments
- figures
- tables
- appendices
- supplementary material, when available

Do not claim to have read unavailable sections, missing appendices, inaccessible supplements, or non-extracted figures. Distinguish paper evidence from interpretation and mark inferred relevance as inference.

## Report Output

Produce valid HTML in Traditional Chinese for a PhD-level reader. The report should be substantially more detailed than a daily multi-paper summary and may exceed 5,000 Chinese words when the paper warrants it.

Use semantic HTML:

```html
<article>
  <h1></h1>
  <section></section>
  <h2></h2>
  <h3></h3>
  <table></table>
  <figure></figure>
  <figcaption></figcaption>
</article>
```

Use MathML for important formulas:

```html
<math xmlns="http://www.w3.org/1998/Math/MathML">
  ...
</math>
```

For HTML report formulas, all displayed equations and inline mathematical variables must be MathML, not LaTeX text, Unicode-only approximations, or `<code>` spans. For piecewise equations, avoid fragile constructs such as `mfenced close=""`; use explicit stretchy brace operators with `mtable`, e.g. a `<mo fence="true" stretchy="true">{</mo>` followed by `<mtable columnalign="left left">...</mtable>`. Wrap wide displayed formulas in an overflow-safe container so they scroll horizontally instead of breaking the page layout. Before delivery, validate that MathML opening and closing tags match, no unresolved formula placeholders remain, and equations render without overflowing the report.

Use base64-encoded embedded images for figures whenever extraction is possible:

```html
<img src="data:image/png;base64,..." alt="Figure description">
```

If figure extraction is impossible, describe the figure from the paper text and explicitly state that the original image could not be embedded.

## Required Sections

### 1. Executive Summary

Include:

- one-page high-level summary
- main contributions
- why the paper matters

### 2. Research Context

Include:

- background
- prior work
- technical motivation
- problems the paper tries to solve
- comparison with previous approaches

### 3. Method Deep Dive

Include:

- detailed architecture walkthrough
- every major module explained
- training pipeline
- inference pipeline
- data flow through the model

### 4. Formula Analysis

For every important equation:

- show the original equation using MathML
- explain every symbol
- explain the physical, statistical, or computational meaning
- explain why the equation is needed
- explain how it affects optimization or representation learning
- explain connections to prior methods

### 5. Architecture Figures

Include:

- original figures from the paper whenever possible
- base64-embedded figure images whenever extraction is possible
- detailed explanation of each figure
- information flow
- architectural design choices

### 6. Experimental Analysis

Include:

- datasets
- evaluation protocols
- baselines
- metrics
- result tables
- detailed interpretation of results
- failure cases
- error analysis

### 7. Ablation Study Analysis

Include:

- every ablation
- what was removed or changed
- performance impact
- why performance changed
- what conclusions can and cannot be drawn

### 8. Reproducibility

Include:

- hyperparameters
- training details
- compute requirements
- released code and data
- preprocessing
- implementation pitfalls
- missing details that may block reproduction

### 9. Critical Review

Include:

- strengths
- weaknesses
- hidden assumptions
- scalability issues
- generalization concerns
- practical deployment challenges

### 10. Audio Deepfake Detection Relevance

Even if the paper is not directly about audio deepfake detection, analyze:

- which ideas could transfer
- which modules could be reused
- which representations are likely useful
- possible adaptation to spoofing, synthetic speech, replay, or voice conversion detection
- robustness implications
- potential future research directions

Clearly label this section as inferred when the paper is not directly about audio deepfake detection.

### 11. Research Notes

Include:

- key takeaways
- open questions
- possible follow-up experiments
- ideas for extending the work
- reproduction checklist

## Quality Rules

- Stay scoped to exactly one paper.
- Preserve the user's requested lens, such as methods, implementation, business implications, reproducibility, or audio deepfake detection.
- Prefer page, section, figure, equation, and table references when available.
- Explain tables in prose instead of only reproducing numbers.
- Discuss negative or missing results when the paper provides enough evidence.
- Be explicit when details are unavailable.
- Avoid unsupported claims, invented citations, and generic praise.
