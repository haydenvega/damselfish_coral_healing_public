# How to Respond to Reviewers

A short primer on the craft of writing responses to peer review. Developed during the revision of this manuscript (RSBL-2026-0177); the principles generalize.

The `response_to_reviewers.md` in this directory is a worked example written to the standards below.

---

## The job

A response-to-reviewers document does two things at once:

1. **Convinces the editor** the paper is now acceptable.
2. **Convinces the reviewers** their time wasn't wasted.

Those are different audiences with different needs. The editor scans for "addressed / not addressed / still contentious." The reviewer wants to see their specific comment was understood and acted on. Write so both can find what they need fast.

---

## Tone

**Grateful, not obsequious.** "Thanks" is enough. Strip every:

- "We are deeply grateful for…"
- "We thank the Referee for this insightful comment…"
- "We appreciate the rigor of this review…"

These read as filler. Worse — they read as deflection. Lead with what you did, not how you feel about being asked.

**Confident, not defensive.** When the reviewer is right, say so once and move on. Don't apologize at length. When they're wrong, push back precisely. Don't bluster.

**Match the level of formality of the reviewers' comments.** If R1 wrote in dense scientific prose, your response should too. If R2 wrote casually with "I'd also like to see…", your response can be a touch more casual. Mirror them.

---

## Three response modes

Almost every reviewer comment falls into one of three categories. Decide which mode each comment belongs to *before* drafting your response.

### 1. Implement (60–80% of comments)

The reviewer asked for something reasonable. You did it. Response is short:

> *"Done. Lines 134 of the revised Methods now state X."*

That's it. No padding. The reviewer can verify by opening the manuscript.

**Common cases:** wording fixes, missing citations, methods clarifications, formatting compliance, adding supplementary detail.

### 2. Show (10–20% of comments)

The reviewer raised a concern that needs new analysis to answer — and the answer might be "you were right, here's the fix" or "we checked, no problem." Either way, **run the analysis and report what you found.** Don't argue.

> *"We agree this needed checking. After excluding the 8 algae-colonized corals, the fish × wound interaction held: χ²₂ = 10.25, p = 0.006. Cell means shifted by ≤ 0.018 Fv/Fm units. The primary conclusion is preserved."*

**Show is always more persuasive than argue.** When in doubt, run the analysis.

**Common cases:** sensitivity analyses, robustness checks, alternative model specifications, requests to test an assumption.

### 3. Push back (≤ 5% of comments)

You actually disagree on substance, and the reviewer is wrong. This is rare. Use it sparingly — you usually get one "respectful disagreement" per response without irritating the editor. Save it for cases where:

- The reviewer misunderstood your design or methods.
- The reviewer is asking you to do something that would change the paper's scope.
- The reviewer wants a test that isn't statistically appropriate.

Structure:

1. Acknowledge their point in their own words.
2. Explain *why* you're doing something different.
3. Offer a partial compromise where possible (e.g., "we don't think a Cox model is necessary, but we have added a sentence acknowledging the censoring direction").

Never just say "we disagree." Always show your work.

In this revision, every reviewer comment fell into Implement or Show. No Push back was warranted — both reviewers were reasonable and most comments improved the paper.

---

## Sentence structure for each response

Use this template:

```
> [Quote the reviewer verbatim — block quote]

[Brief acknowledgment or skip straight to action.]

[What you did. Be specific.]

[Where in the manuscript / supplementary material the reviewer can verify.]
```

**Good example** (from your R1.4 response):

> *"This deserves a formal quantitative comparison — a Fisher's exact test would be appropriate."*

Promoted to a formal analysis. Among the 48 wounded corals, two-tailed Fisher's exact: OR = 0.11 (95% CI: 0.00–0.99), p = 0.048. Reported in Results at lines 168–172 and as new Supplementary Table S2.

**Bad example** (same point, padded):

> *"This deserves a formal quantitative comparison — a Fisher's exact test would be appropriate."*

We thank the Referee for this excellent suggestion, which has substantially strengthened our reporting of this important result. In response to this thoughtful comment, we have now conducted a formal Fisher's exact test, which we agree is the appropriate statistical approach for these data. The results, which we now report in detail, show that…

The second version says nothing the first doesn't, but takes 4× longer to read.

---

## What reviewers really want

When you read a reviewer comment, ask yourself:

1. **What did they literally ask for?**
2. **What's the underlying concern?** Sometimes the literal request is a proxy for a deeper worry. R1's REML/ML comment was literally "report which estimation method you used," but the underlying concern was "your p-values might be invalid." Addressing only the literal request looks evasive. Address both.
3. **Are they asking me to do something, or to acknowledge something?** Acknowledgments are cheap — a sentence in the Discussion is usually enough. Doing something means analysis or text changes.

Most reviewer frustrations come from authors addressing the literal question while ignoring the underlying concern.

---

## Specific pitfalls to avoid

1. **Don't oversell your revisions.** "We have substantially improved the manuscript" reads as defensive. The reviewer will judge whether you've improved it.
2. **Don't apologize for the original.** "We apologize for not initially clarifying" is unnecessary. Just clarify.
3. **Don't list things you *could* do but didn't.** If you ran a sensitivity analysis, report it. If you didn't, don't mention it.
4. **Don't quote the reviewer and then ignore part of what they said.** If they made three points in one paragraph, address all three.
5. **Don't write a long response to a small comment.** A typo fix needs one sentence: "Corrected." Long responses to small comments signal nervousness.
6. **Don't use words like "novel," "groundbreaking," "important."** Let your work speak for itself.
7. **Don't blame your coauthors.** "An earlier draft mistakenly stated X" is fine. "Coauthor Y inserted this" is not.

---

## Pre-submission checklist

Before you click submit:

- [ ] Every reviewer comment has a numbered response.
- [ ] Every response says what you *did*, not what you *think*.
- [ ] Every claim about a manuscript change cites a specific line number.
- [ ] New analyses report test statistic, df, p-value, and effect size or CI.
- [ ] No "we are grateful," "we appreciate," "groundbreaking," "novel."
- [ ] Read the whole response aloud. If it sounds like a corporate press release, cut.
- [ ] Coauthors have reviewed.
- [ ] Cover letter mentions: deadline acknowledged, figure ownership, what major changes were made.

---

## One more thing

Reviewers are usually right about *what's wrong* with a paper, even when they're wrong about *how to fix it*. Treat their comments as diagnoses. The treatment is yours to design.
