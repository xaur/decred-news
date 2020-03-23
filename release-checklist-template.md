# Release checklist

Checklist that is currently in use. For ideas see [release-checklist-ideas.md](release-checklist-ideas.md).

Legend: `(opt)` - optional steps, `by: X` - execute step by date X, `ready by: X` - resource must be ready by date X, `PO` - product owner responsible for the overall quality.

Copy the raw Markdown below into a new issue.

---

**DRAFT**: {link}

**Dependencies**: Send notice in advance so that people can plan their work.

- [ ] Title image via an [issue in dcrdesign](https://github.com/decred/dcrdesign/issues) (notify by: 20th, ready by: 3rd)
  * GitHub version must be 768x384 px
  * ask for image title and description (saender)
- [ ] first time contributors (degeri or s_ben)
- [ ] dev activity stats (degeri or s_ben)
- [ ] PR update (l1ndseymm, notify by: 28th, ready by: 3rd)
- [ ] Outreach update (Dustorf, notify by: 28th, ready by: 3rd)

**End of month snapshots**: Snapshot data that is hard to obtain later.

- [ ] snapshot social media stats
  * Politeia, Matrix, Discord, Telegram, Twitter, Reddit, YouTube, Facebook, LinkedIn, GitHub dcrd, Instagram
  * very helpful: http://dcrextdata.planetdecred.org/community
  * (opt) non-English platforms: Telegram (es pt zh it ru), Twitter (es), Instagram
- [ ] staking
  * 30-day average ticket price (https://dcrstats.com)
- [ ] nodes
  * node count, versions, etc (https://charts.dcr.farm/)

**Release**

- [ ] Extract more dev updates from GitHub repos
- [ ] Complete Development (by: 2nd)
- [ ] Complete People (by: 2nd)
- [ ] PO review Development and People
- [ ] Ask in #dev to review Development and People
- [ ] Complete Events
- [ ] (opt) Ask #events to review Events
- [ ] Complete Outreach
- [ ] Complete Media
- [ ] (opt) Ask #marketing to review Outreach+Events+Media
- [ ] Complete Governance
- [ ] Complete Network
- [ ] Complete Integrations, Adoption
- [ ] (opt) Find interesting Reddit and Twitter threads
- [ ] Complete Community Discussions
- [ ] Complete Markets
- [ ] Complete Relevant External
- [ ] (opt) Ask quoted people to review their texts
- [ ] Complete Intro
- [ ] PO review of all sections
- [ ] Ask #writers to review (by: 3rd)
- [ ] Incorporate all feedback
- [ ] Resolve all [TODOs](https://github.com/xaur/decred-news/blob/docs/guidelines.md#todos)
- [ ] Carefully check that all people who contributed or gave feedback are in [credits](https://github.com/xaur/decred-news/blob/docs/guidelines.md#how-to-give-credit)
- [ ] [Lint](https://github.com/xaur/decred-news/blob/docs/guidelines.md#linting)
- [ ] Add [title image](https://github.com/xaur/decred-news/blob/docs/guidelines.md#title-image)
- [ ] Remove `{DRAFT}` from title
- [ ] Pre-release review: check spelling, grammar, test that links work
- [ ] Publish on GitHub with a single commit to `gh-pages`
- [ ] Publish on Medium (richardred or Haon)
- [ ] (opt) Verify Medium version, check for formatting issues
- [ ] Submit Medium link to r/decred
- [ ] Tweet Medium link via decredproject. Don't forget to add title image. (by: 6th)
- [ ] If changes are necessary after the release, add commits to `gh-pages` (test in `draft` if needed) and update Medium
- [ ] [Update index](https://github.com/xaur/decred-news/blob/docs/guidelines.md#updating-index)
- [ ] Fast-forward `master` to `gh-pages`
- [ ] Create Git tag from the draft branch, e.g. `archive/draft1901`
- [ ] Delete the draft branch
- [ ] (opt) Update `journal-template.md` in `docs` branch
- [ ] (opt) Update this release checklist template in the `docs` branch
- [ ] Start the new cycle
