---
name: verify-ai-citations
description: Verify academic citations, quotations, attributions, claim-source relationships, and whether definite claims have independent primary corroboration. Use when the user asks to verify a specific claim (such as “求证某观点”), a paper, citation, or quotation, even without naming a source or this skill. Also use before presenting a definite substantive claim derived from web search, including in an answer to an ordinary question, and when presenting scholarly sources found through web search. Distinguish independent original sources from repetition and always disclose evidence access level.
---

# AI Citation Verification

Treat each **claim and its cited or discovered evidence** as the unit of verification. Do not treat finding a paper as reading it, or a working link as proof that the paper supports the claim.

## Workflow

1. Split compound statements into separate verifiable claims.
2. Record the access level before interpreting the source:
   - **Full text read**: read enough relevant Methods, Results, tables, figures, or limitations to judge the claim in context.
   - **Abstract only**: read only the abstract; do not infer details absent from it.
   - **Secondary citation**: learned about the original through another source; name the chain when relevant.
   - If weaker, state **Metadata only**, **Search snippet only**, **References/endnotes only**, or **Citation discovered only**.
3. Verify in order:
   - **Existence**: Does the work exist in an authoritative index, publisher site, or repository?
   - **Bibliographic accuracy**: Do title, authors, year, venue, and DOI/PMID/ISBN match? A real identifier pointing to a different paper fails this check.
   - **Claim support**: Does the accessible text support the exact claim?
   - **Source relevance**: Is this an appropriate source for that claim?
4. For claim support, compare population, construct, intervention/exposure, outcome, direction, magnitude, statistics, causality, generalization, mechanism, and limitations when relevant.
5. Trace striking claims through secondary citations toward the earliest accessible primary source. Do not treat repetition as verification.
6. If evidence is insufficient, return **Cannot verify**. Never upgrade uncertainty because the title, abstract, or link looks plausible.

## Independent Primary Corroboration

Apply this check to each specific claim the user asks to verify and, **before answering**, to each definite substantive conclusion drawn from web search. This includes claims stated without an attached citation. Split a mechanism claim into its observable effect and proposed mechanism; corroboration of the effect alone does not corroborate the mechanism.

1. Trace each supporting page's citation or evidence chain to the underlying original research, original text, dataset, official record, or firsthand documentation. For original research, check that the source actually reports evidence for the **same precise claim**, at the available access level.
2. Count **independent evidentiary origins**, not URLs, authors, outlets, papers, or reviews. Multiple articles citing one experiment, papers reanalyzing the same dataset, a press release about its paper, and an institution reposting that release count as **one** origin. A review or meta-analysis helps locate originals but is not itself an additional original study. Distinct studies using the same dataset are not independent data replications for that result. Check shared samples, data, methods, citations, and institutional source chains where possible.
3. List the counted origins with links and access labels; identify repeated or derivative sources separately when they could create a false impression of consensus. Do not assume independence merely because authors or publishers differ. If lineage cannot be determined, label it **independence unclear** and exclude it from the verified count.
4. Report **“X个独立原始来源”** (with the verified count) or **“未找到其他独立原始来源”** when only one origin is found; if no original has been verified, say **“0个已核实的独立原始来源”**. A search cannot establish that no other source exists: state the search scope or access limit briefly. Distinguish multiple independent sources from convergent support; if findings conflict or address different claims, explain that rather than adding them together.
5. Calibrate the conclusion to the verified originals and their quality. A single original can support a narrow claim; more independent originals do not by themselves establish causation, a neural mechanism, or scientific consensus. If the count is uncertain, state a lower bound rather than invent a precise number.

## Quotation and Attribution Checks

For a request to verify a sentence, quotation, saying, aphorism, or famous line, invoke this skill automatically even if the user only asks for its “source” or names a possible author.

1. Treat **wording + speaker/author + work + location + context** as separate claims.
2. Search toward the earliest authoritative primary text in the original language. Prefer a critical edition, manuscript/archive, first or authoritative edition, or a reliable full-text repository.
3. Record separately what was directly read:
   - original-language primary text;
   - published translation;
   - authoritative secondary quotation;
   - bibliographic metadata only.
   Never present these as the same access level.
4. Compare the circulating wording with the primary text. State whether it is verbatim, a faithful translation, a shortened excerpt, a paraphrase, a composite, a mistranslation, or falsely attributed.
5. Read enough surrounding text to explain omissions or shifts in meaning. Check whether a standalone “famous quote” was cut from a longer sentence or argument.
6. Verify the most precise stable locator available: edition, volume, chapter/section, page, paragraph, line, or canonical scholarly locator. Do not invent a page number or transfer pagination across editions.
7. If the original-language text was read but the cited translation was only found inside a secondary source, label them separately, for example: **Original: Full text read; English translation: Secondary citation**.
8. Conclude with a compact verdict: authentic or not; attribution and work correct or not; exact quotation versus shortened/paraphrased wording; and the main contextual caveat.

## Ratings

- **Existence**: Verified / Probably verified / Unverified / Hallucinated
- **Bibliographic accuracy**: Accurate / Partial / Inaccurate
- **Claim support**: Direct / Partial / Indirect / Contradictory / Cannot verify
- **Source relevance**: High / Moderate / Low / Inappropriate

Keep evidence access separate from scientific quality. Full access to a weak study does not make it strong evidence.

## Output

For each important claim, report compactly (omit bibliographic fields when no specific work was cited):

```text
Citation:
Access level:
Existence:
Bibliographic accuracy:
Claim:
Claim support:
Source relevance:
Evidence and caveat:
Independent primary origins: X个独立原始来源 / 未找到其他独立原始来源 / 0个已核实的独立原始来源 (links and access labels; derivatives or uncertain lineages separately)
Verdict:
```

用户未指定文献时，可以省略逐篇书目信息的完整核对；但凡用某项找到的研究支撑关键结论，仍须逐项标明读取层级、它支持的是哪个具体主张、支持程度及主要局限。多项研究可用紧凑表格呈现，不必重复完整核验模板。

Place the access label beside every scholarly link used in a research answer. Distinguish what the source states from what you infer. Do not silently replace a weak citation with a stronger one; explain the replacement.
