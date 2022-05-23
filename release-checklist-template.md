# Release checklist

Checklist currently in use. For unused ideas see [release-checklist-ideas.md](release-checklist-ideas.md).

Legend: `by: X` - execute step by date X, `ready by: X` - resource must be ready by date X, `PO` - product owner responsible for the overall quality.

Copy the raw Markdown below `---` into a new release GitHub issue or pull request.

---

**DRAFT**: {link}

**Usage**: This list is a soft reminder. Some tasks may be skipped when not needed or short on time.

**Monthly snapshots**: Snapshot data that is hard to obtain later. Ideally, capture it at 1st day of the month at 00:00 UTC.

- [ ] social media stats for People
- [ ] mining stats
  - absolute Ph/s and network share % values as _reported_ by pools and dashboards
  - counts of blocks _actually mined_ in a certain timeframe
  - [miningpoolstats.stream](https://miningpoolstats.stream/decred)
  - [dcrstats.com/pow](https://dcrstats.com/pow)
- [ ] staking stats
  - ticket price [30-day average](https://dcrstats.com)
- [ ] node stats
  - [Decred Mapper](https://nodes.jholdstock.uk/user_agents)
  - [PD Analytics](https://analytics.planetdecred.org/nodes)
- [ ] VSP stats
  - rendered: [decred.org/vsp](https://decred.org/vsp/)
  - API: [legacy](https://api.decred.org/?c=gsd), [current](https://api.decred.org/?c=vsp)
- [ ] [LN stats](https://ln-map.jholdstock.uk/)

**Writing**

- [ ] request a PR update for Outreach in advance
- [ ] scan GitHub repos for dev updates
  - make notes of new names for first-time contributors
- [ ] complete Development
- [ ] complete People
- [ ] PO review Development and People
- [ ] ask in #dev to review Development and People
- [ ] ask in #planetdecred to review Development
- [ ] complete Governance
- [ ] complete Network
- [ ] scan Twitter for notable news
- [ ] scan Reddit for notable news
- [ ] complete Ecosystem
- [ ] complete Events
- [ ] ask #events to review Events
- [ ] complete Media
- [ ] complete Outreach
- [ ] ask #marketing to review Outreach+Events+Media
- [ ] complete Markets
- [ ] complete Relevant External
- [ ] offer quoted people to review their texts
- [ ] complete Intro
- [ ] PO review of all sections
- [ ] incorporate all feedback
- [ ] resolve all [TODOs](https://github.com/xaur/decred-news/blob/docs/guidelines.md#todos)
- [ ] ensure that all people who contributed or gave feedback are in [credits](https://github.com/xaur/decred-news/blob/docs/guidelines.md#how-to-give-credit)
- [ ] add [title image](https://github.com/xaur/decred-news/blob/docs/guidelines.md#title-image)
- [ ] add other images with captions
- [ ] almost final review: grammar, test that links work
- [ ] [lint](https://github.com/xaur/decred-news/blob/docs/guidelines.md#linting)
- [ ] remove `{DRAFT}` from title
- [ ] final auto grammer check

**Publishing**

- [ ] publish on xaur.github.io with a single commit to `gh-pages`
- [ ] add all images to the [files repo](https://github.com/xaur/decred-journal-files)
- [ ] publish on Medium
  - upload images
  - make Table of Contents
  - add to `/decred/journals`
  - add relevant tags
  - verify text previews shown at `/decred` and `/decred/journals`
  - check for formatting issues
- [ ] post Medium link on r/decred
- [ ] tweet via decredproject
  - add correct title image for Twitter
- [ ] announce on: Matrix #dcr, t.me/DCRann, Blockfolio, CoinGecko
- [ ] announce on Instagram
- [ ] publish on Odysee
  - prepare Odysee-specific markdown, add to the [extras repo](https://github.com/xaur/decred-journal-extra)
  - use this pattern for post ID: `decred-journal-YYYY-MM`
- [ ] fast-forward `master` to `gh-pages` (so that translators can get it from `master`)
- [ ] if changes are needed after the release, add commits to `gh-pages` (test in `draftXX` if needed), `master` and update other places
- [ ] add new issue to decred.org Press page
  - submit a PR to edit [coverage.yml](https://github.com/decred/dcrweb/blob/master/src/data/press/coverage.yml)
  - verify deployment to decred.org
- [ ] [update index](https://github.com/xaur/decred-news/blob/docs/guidelines.md#updating-index)

**Housekeeping**

- [ ] archive draft history
  - create `tmp` at `master`, merge both `drafts` and the latest draft commit, fast-forward `drafts` to `tmp`
- [ ] update `journal-template.md` in the `docs` branch
- [ ] update `release-checklist-template.md` in the `docs` branch
- [ ] start new cycle
- [ ] delete the draft branch (will auto-close the PR)
