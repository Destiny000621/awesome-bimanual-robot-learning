# Contributing

Thank you for helping maintain Awesome Robot Learning for Bimanual Manipulation.

## Adding a Paper

Before opening a pull request:

1. Confirm that the paper explicitly studies bimanual or dual-arm robot learning, introduces a relevant dataset or benchmark, or provides substantive bimanual evaluation.
2. Search the README for the title and arXiv identifier to avoid duplicates.
3. Verify the title, venue, year, and links against the paper or official project page.
4. Add the paper to its primary methodological section and keep entries ordered newest first.
5. Mark general methods as `Bimanual-evaluated` when bimanual manipulation is not their central subject.

Use this format:

```markdown
- **Paper Title**. *Venue, Year.* [[paper](URL)] [[project](URL)] [[code](URL)] `Tag1` `Tag2`
```

## Suggested Tags

`FM`, `LLM`, `VLM`, `VLA`, `WM`, `Diffusion`, `Flow`, `IL`, `RL`, `Planning`, `Scheduling`, `Representation`, `Dataset`, `Benchmark`, `Real`, `Sim`, `Sim-to-Real`, `Humanoid`, `Dexterous`, `Tactile`, `Deformable`, `Safety`

## Quality Guidelines

- Prefer official arXiv, publisher, project, and code links.
- Do not copy abstracts into the README.
- Avoid promotional descriptions or unverified performance claims.
- Keep a paper in one primary section; use tags to express overlapping methods.
- Preprints are welcome and should be labeled `arXiv`.
- Workshop papers and technical reports are welcome when clearly labeled.
