# Release checklist

Checklist that is currently in use. For ideas see [release-checklist-ideas.md](release-checklist-ideas.md).

Legend: `(opt)` - optional steps, `by: X` - execute step by date X, `ready by: X` - resource must be ready by date X, `PO` - product owner responsible for the overall quality.

Copy the raw Markdown below into a new issue.

---

**DRAFT**: {link}

**Dependencies**: Send notice in advance so that people can plan their work.

- [ ] title image via an [issue in dcrdesign](https://github.com/decred/dcrdesign/issues) (notify by: 20th, ready by: 3rd)
- [ ] first time contributors
- [ ] dev activity stats
- [ ] PR update (notify by: 28th, ready by: 3rd)

**End of month snapshots**: Snapshot data that is hard to obtain later.

- [ ] social media stats
  - at the very minimum, snapshot stats reported in People
  - (opt) snapshot all accounts tracked by [social-media-stats](https://github.com/decredcommunity/social-media-stats) repo
- [ ] mining: absolute and share% pool hashrate values
  - https://miningpoolstats.stream/decred
  - https://dcrstats.com/pow
- [ ] staking
  - 30-day average ticket price (https://dcrstats.com)

**Writing**

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
- [ ] (opt) Ask #writers to review (by: 3rd)
- [ ] Incorporate all feedback
- [ ] Resolve all [TODOs](https://github.com/xaur/decred-news/blob/docs/guidelines.md#todos)
- [ ] Ensure that all people who contributed or gave feedback are in [credits](https://github.com/xaur/decred-news/blob/docs/guidelines.md#how-to-give-credit)
- [ ] [Lint](https://github.com/xaur/decred-news/blob/docs/guidelines.md#linting)
- [ ] Add [title image](https://github.com/xaur/decred-news/blob/docs/guidelines.md#title-image)
- [ ] Remove `{DRAFT}` from title
- [ ] Pre-release review: check spelling, grammar, test that links work

**Publishing**

- [ ] Publish on GitHub with a single commit to `gh-pages`
- [ ] Publish on Medium
  - add to /decred/journals
  - add relevant tags
  - test short preview shown at /decred and /decred/journals
  - check for formatting issues
- [ ] Publish on Publish0x
  - add relevant tags
- [ ] Submit Medium link to r/decred
- [ ] Tweet Medium link via decredproject. Don't forget to add title image. (by: 6th)
- [ ] Submit new issue to decred.org Press page ([example](https://github.com/decred/dcrweb/pull/898))
- [ ] Publish on CoinMarketCap
- [ ] If changes are necessary after the release, add commits to `gh-pages` (test in `draftXX` if needed) and update other places
- [ ] [Update index](https://github.com/xaur/decred-news/blob/docs/guidelines.md#updating-index)
- [ ] Fast-forward `master` to `gh-pages`

**Housekeeping**

- [ ] Create archiving Git tag from the draft branch, e.g. `archive/draft1901`
- [ ] Delete the draft branch
- [ ] (opt) Update `journal-template.md` in `docs` branch
- [ ] (opt) Update this `release-checklist-template.md` in the `docs` branch
- [ ] Start new cycle
